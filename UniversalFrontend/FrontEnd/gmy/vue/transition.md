 transition内置的组件

```
App.vue
<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link>|
      <router-link to="/about">About</router-link>
    </div>
    <transition :name="move">
      <!-- keepalive和动画一起使用 动画要放到外层 -->
      <router-view />
    </transition>
  </div>
</template>
<script>
export default {
  data() {
    return {
      a: { name: 1 },
      move: "slide-left" // 动画样式
    };
  },
  watch: {
    $route: {
      handler(to, from) {
        // 通过路由判断动画向左还是向右
        if (to && from) {
          if (to.meta.idx > from.meta.idx) {
            // 后面比前面大 做向左的动画
            this.move = "slide-left";
          } else {
            // 否则是向右的动画
            this.move = "slide-right";
          }
        }
      },
      immediate: true // 立即执行handler
      // deep: true, // 深层监控
      // lazy: true, // 懒加载 computed有缓存
    }
  }
};
</script>
<style lang="less">
.slide-left-enter,
.slide-left-enter-active,
.slide-right-enter,
.slide-right-enter-active {
  transition: all 0.5s;
}
.slide-left-enter,
.slide-right-leave-to {
  transform: translate(-100%);
}
.slide-left-leave-to,
.slide-right-enter {
  transform: translate(100%);
}
</style>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```
router/index.js
import Vue from "vue";
import VueRouter from "vue-router";
import Home from "../views/Home.vue";
import lazyC from "../lib/util";
Vue.use(VueRouter);
const routes = [
  {
    path: "/",
    name: "home",
    component: Home,
    meta: {
      idx: 0
    }
  },
  {
    path: "/about",
    name: "about",
    meta: {
      idx: 1
    },
    component: lazyC(() => import("../views/About.vue"))
  }
];
const router = new VueRouter({
  routes
});
export default router;
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```
lib/util.js
import loading from "../components/Loading.vue";
const layC = asyncFunction => {
  const component = () => ({
    component: asyncFunction(),
    loading
  });
  // layC最后要返回一个组件 cli 不支持template模板
  return {
    render: h => h(component)
  };
};
export default layC;

components/Loading.vue
<template>
  <div>...加载中</div>
</template>
```