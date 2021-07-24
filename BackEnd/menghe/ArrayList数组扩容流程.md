## ArrayList数组基础属性
* DEFAULT_CAPACITY：默认容器大小，使用new创建ArrayList时不会初始化容器的容量
* MAX_ARRAY_SIZE：Integer.MAX_VALUE - 8;   容器最大容量

## 代码流程
```java
 public boolean add(E e) {
     modCount++; // 这个暂时没有研究
     add(e, elementData, size);
     return true;
}
```

```java 
private void add(E e, Object[] elementData, int s) {
	// 如果size和容器容量相等表示需要扩容 执行grow方法
    if (s == elementData.length)
        elementData = grow();
    elementData[s] = e;
    size = s + 1;
}
```

```java 
private Object[] grow() {
    return grow(size + 1);
}

private Object[] grow(int minCapacity) {
    return elementData = Arrays.copyOf(elementData, newCapacity(minCapacity));
}

// 计算新的容器容量
private int newCapacity(int minCapacity) {
    // overflow-conscious code
    int oldCapacity = elementData.length;
    // 新容器的容量约为 旧容器容量*1.5
    int newCapacity = oldCapacity + (oldCapacity >> 1);
    // 此处在容器容量为0的时候执行代码（创建ArrayList时未指定长度）
    if (newCapacity - minCapacity <= 0) {
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA)
            return Math.max(DEFAULT_CAPACITY, minCapacity);
        if (minCapacity < 0) // overflow
            throw new OutOfMemoryError();
        return minCapacity;
    }
    
    return (newCapacity - MAX_ARRAY_SIZE <= 0)
        ? newCapacity
        : hugeCapacity(minCapacity);
```

```java 
Arrays.java
public static <T> T[] copyOf(T[] original, int newLength) {
    return (T[]) copyOf(original, newLength, original.getClass());
}
public static <T,U> T[] copyOf(U[] original, int newLength, Class<? extends T[]> newType) {
    @SuppressWarnings("unchecked")
    T[] copy = ((Object)newType == (Object)Object[].class)
        ? (T[]) new Object[newLength]
        : (T[]) Array.newInstance(newType.getComponentType(), newLength);
    // 使用System.arraycopy方法将旧的数据拷贝至新的容器中
    System.arraycopy(original, 0, copy, 0,
                     Math.min(original.length, newLength));
    return copy;
```
* src - 源数组。
* srcPos - 源数组中的起始位置。
* dest - 目标数组。
* destPos - 目的地数据中的起始位置。
* length - 要复制的源数组元素的数量。