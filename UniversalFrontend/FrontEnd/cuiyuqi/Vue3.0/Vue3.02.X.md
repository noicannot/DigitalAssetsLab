 1.生命周期函数 

> vue2.0-->vue3.0
>
> beforeCreate->setup
>
> created->setup
>
> beforeMount->onBeforeMounted
>
> mounted -> onMounted
>
> beforeUpdate-onbeforeupdate
>
> updated->onupdated
>
> beforedestory->onBeforeUnmounte
>
> destory->onUnmounted

2.注册组件

**vue2.0**

```
Vue.component('button-counter', {
  data: () => ({
    count: 0
  }),
  template: '<button @click="count++">Clicked {{ count }} times.</button>'
})
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**vue3.0**

> 调用 `createApp` 返回一个*应用实例*，这是 Vue 3 中的新概念：

```
import { createApp } from 'vue'

const app = createApp({});
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3.组件上的v-model方法已更改 替换v-bind.sync

> 现在可以在一个组件上使用多个v-model进行双向绑定
>
> 也可以自定义v-model 修饰符

**vue2.x**

```
在组件上使用v-model 相当于绑定value prop和input事件
<ChildComponent :value="pageTitle" @input="pageTitle = $event" />
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**vue3.x**

```
在 3.x 中，自定义组件上的 v-model 相当于传递了 modelValue prop 并接收抛出的 update:modelValue 事件：
<ChildComponent v-model="pageTitle" />

<!-- 是以下的简写: -->

<ChildComponent
  :modelValue="pageTitle"
  @update:modelValue="pageTitle = $event"
/>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

4.v-for 上面的key 

vue2.x

```
在 Vue 2.x 中 <template> 标签不能拥有 key。不过你可以为其每个子节点分别设置 key。
<template v-for="item in list">
  <div :key="'heading-' + item.id">...</div>
  <span :key="'content-' + item.id">...</span>
</template>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

vue3.x

```
<template v-for="item in list" :key="item.id">
  <div>...</div>
  <span>...</span>
</template>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 5.v-if 和v-for 优先级发生变化

```
2.x 版本在一个元素上同时使用v-if  和 v-for,v-for会优先作用
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```
3.x中v-if 总是优先于 v-for
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)