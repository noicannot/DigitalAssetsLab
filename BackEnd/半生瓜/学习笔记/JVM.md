## JVM

三种JVM

sum公司:Hotsopt

BEA:JRockit

IBM:J9

![image-20210413161147681](http://47.101.69.157:8111/s/Z7Gm6Cnm6JtSktj/preview)



#### 类加载器

![image-20210413160935953](http://47.101.69.157:8111/s/wBq9KeLQ5iaJWq5/preview)

​	作用：加载Class文件

1.虚拟机自带的加载器

2.启动类加载器

3.扩展类加载器

4.应用程序加载器

双亲委派机制：

​	1、类加载器收到类加载请求.

​	2、将这个请求向上委托给父类加载器去完成，一直向上委托，直到启动类加载器

​	3、启动加载器检查是否能够加载当前这个类，能加载就结束，使用当前的加载器，否则，抛出异常通知子类加载器进行加载

​	4、重复步骤 3

注：	null：java调用不到   java底层时用C写的 		JAVA = C++--

![img](http://47.101.69.157:8111/s/wyJFfGn9Tg3DwdF/preview)

​		沙箱安全机制

![image-20210413162244193](http://47.101.69.157:8111/s/r86ft3wWRnQPj63/preview)

![image-20210413162604988](http://47.101.69.157:8111/s/Ery74ZrJWAHx6FP/preview)

​	Native：

![image-20210413165019269](http://47.101.69.157:8111/s/ZSiwdtC9aTWPkfE/preview)

解决方案：

​		HTTPResful、Socket, WebService



![image-20210413164344351](C:\Users\dell\Desktop\DigitalAssetsLab\BackEnd\yezhiming\preview)



#### 方法区

Method Area 方法区

​	方法区是被所有线程共享，所有字段和方法字节码，已经一下特殊方法，如构造函数，接口代码也在此定义，简单说，所有定义的方法的信息都保存在该区域，此区域属于共享区间；静态变量、常量、类信息(构造方法、接口定义)、运行时的常量池存在方法区中，但时，实例变量存在堆内存中，和方法区无关。字符串在常量池里

### 		栈

​	程序 = 数据结构 + 算法

  栈：先进后出,后进先出			队列：先进先出，后进后出

栈：栈内存，主管程序的运行，生命周期和线程同步；

线程结束，栈内存也就释放，对于栈来说。不存在垃圾回收问题

栈：八大基本数据类型	+	对象引用	+	实例方法

栈运行原理：栈帧

栈内存满了：StackOverflowError

栈	+	堆 	+ 方法区：交互关系

Java本质是值传递

### 堆

Heap,一个JVM只有一个堆内存，堆内存是可以进行调节的。

类加载器读取了类文件后，一般把类，方法，常量 ~，保存所有引用类型的真实对象。

###### 堆内存分为三个对象：

​	1、新生区（伊甸园）： Young/New    轻GC清理

​			类： 诞生和成长的地方，甚至死亡；

​			伊甸园：所有的对象都在伊甸园区new出的

​			幸存者区（0区，1区）：

​	2、老年区：Old	重GC清理（FullGC）

​	3、永久区：Pelm	

​		这个区域常驻内存中，用来存放JDK自身携带的Class对象。	接口元数据，存储的是JAVA运行时的一些环境或类信息~，这个区域不存在垃圾回收，关闭虚拟机就会释放区域内存。

​		一个启动类加载了大量的第三方jar包。tomcat部署了太多的应用，大量动态生成的反射类。不断的被加载，直到内存满，就会出现OOM

​		JDK1.6:  永久代，常量池是在方法区钟

​		JDK7：  永久代，慢慢退化（提出去永久代）,在堆中

​		JDK8:	无永久代 名称变为元空间，常量池在元空间

​	元空间逻辑上存在，物理上不存在

###### 	元空间原型图

![image-20210414182742529](http://47.101.69.157:8111/s/9pg97ZCrgZZ8sxn/preview)

###### jdk7堆原型图

![image-20210414175822852](http://47.101.69.157:8111/s/w52HkWfyysWMrX4/preview)

GC垃圾回收主要时在伊甸园区和养老区~

假设内存满了,会报OOM,堆内存不足！Exception in thread "main" java.lang.OutOfMemoryError: Java heap space

![image-20210414180536401](http://47.101.69.157:8111/s/RJBzDSHg3tXmgyB/preview)

在JDK8后，永久存储区改为元空间



![image-20210414180743954](http://47.101.69.157:8111/s/w52HkWfyysWMrX4/preview)

###### 																										JDK8原型图

经研究99%对象都是临时对象！

###### OOM调堆内存:

1.尝试扩大堆内存看结果

2.分析内存看一下哪个地方出了问题

###### 使用Jprofile进行调试

-Xms	设置初始化内存大小：默认为1/64

-Xmx	设置最大分配内存: 	默认为1/4

--XX:+printGCDetails				打印GC垃圾回收信息

--XX:+HeapDumpOnOutOfMemoryError	OOM DUMP

### GC垃圾回收

JVM在进行GC时，并不是对这三个区域统一回收。大部分在新生代回收

​	新生代

​	幸存区(from，to(谁空谁是to))

​	老年代：当一个对象经历了15次GC都还存活，就会放入老年代 

​	调整进入老年代的时间:-XX：-XX:MaxTenuingThreshold

GC两种类: 轻GC（普通GC） 只针对新生代和幸存区 ，每次轻GC清理新生代都会把存活的对象移到幸存区，一旦新生代被GC后，内存就会为空

​				   重GC（全局GC） 新生代和幸存区、老年代



Jvm内存模型和分区,详细到每个区

堆里面的分区有哪些? Eden，from，to，老年代

##### GC算法

标记清除法：

![image-20210415184556969](http://47.101.69.157:8111/s/q7rYWix2G2yj67Y/preview)

优点：不需要额外的空间！

缺点： 两次扫描严重浪费时间，会产生内存碎片。



###### 标记清除压缩算法:

​	再次优化：

​	![image-20210415190053281](http://47.101.69.157:8111/s/ZsBX3YXA64aD897/preview)

###### 复制算法: 

​	为了保证幸存区to区的干净

![image-20210415183612286](http://47.101.69.157:8111/s/e8g8BQFtwMnwxHg/preview)

![image-20210415184130736](http://47.101.69.157:8111/s/TGaK2xNoiDkwk4K/preview)

好处：没有内存的碎片

坏处：浪费了内存空间 ,to区永远是空的。假设对象100%存活（极端情况）

复制算法最佳使用场景：对象存货度较低的情况，新生代



###### 引用计数法: 

​	 用了的对象就留下，没有使用的对象就进行清除

轻GC和重GC分别在什么时候发生？

### 总结

内存效率：复制算法>标记清除算法>标记压缩算法(时间复杂度)

内存整齐度: 复制算法 = 标记压缩算法>标记清除算法

内存利用率:标记压缩算法 = 标记清除算法 >复制算法

GC分代收集算法

新生代:

​	存活率低

​	复制算法

老年带

​	区域大：存活率

​	标记清除(内存碎片不算多) + 标记压缩混合实现



### JMM

1.什么是JMM？

JAVA Memory Model(java内存模型)

2.JMM是干什么的？(官方、博客、视频)

作用：缓存一致性协议，用于定于数据读写的规则（遵守,找到这个规则）。

JMM定义了线程工作内存和主内存之间的抽象关系：线程之间的共享存储在住内存(Main Memory)中,每个线程都有一个私有的本地内存(Local Memory)

解决共享对象可见性问题: Volilate



3.JMM如何学习?

​	JMM是一个抽象的概念，理论

​	![image-20210415193118178](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20210415193118178.png)

​	Volilate：





### 马士兵讲JVM：

##### Hotspot:

​	oracle官方 

##### Jrockit:

​	BEA,曾经号称最快的JVM，后被Oracle收购

##### J9：

IBM

##### Microsoft VM:

##### TaobaoVM:

hotspot深度定制版

##### LiquidVM:

直接针对硬件

##### azul zing:收费产品

最新垃圾回收的业界标杆



单例必须加volatile

##### volatile: 

​	线程见可以见

​	禁止指令重排序

##### G1

###### 三色标记法

​	白色: 未被标记的对象

​	灰色:自身被标记，成员变量未被标记

​	黑色:自身和成员变量均已标记完成

​		 追求响应时间

​		-XX:MaxGCpauseMillis 200

​		对STW进行控制

​	 灵活

​		分Region回收

​		优先回收花费时间少、垃圾比例高的Region

新老年带比例

​	5% - 60%

大对象

​	超过单个Region的50%

###### GC何时触发

​	YGC

​		Edeb空间不足

​		多线程并行执行

​	FGC

​		old空间不足

​		system.gc()

##### G1清除过程：

​			初始标记: 找到根对象，直接引用的对象标记出

​			并发标记: (没有STW) 和应用程序的线程同时进行，使用到就进行标记

​			最终标记: 产生STW， 根据初始标记找到根对象下面引用的对象

​			复制回收: 回收对象时，把用的Region里面的使用对象复制到一个新的Region中，并把原来的Region里面的全部对象进行清除，一个Region最大空间为内存的5%。

​			并行标记: 

##### CMS：

​	并发容器：

##### Serial:



##### 对象创建的过程:
```java
Object o = new Object();
```


###### JDK11最新GC为ZGC

​	设计目标:

​	1.暂停时间不超过10ms

​	2.暂停时间不随堆的大小变化而变化

3. 处理内存从几百M到几个T

