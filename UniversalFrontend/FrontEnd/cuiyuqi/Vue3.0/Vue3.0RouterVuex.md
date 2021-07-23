 **一、VueRouter**

1.新路由器变为 createRouter

```
import { createRouter } from 'vue-router'

const router = createRouter({
  // ...
})
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2.mode的变化

```
该mode: 'history'选项已被更灵活的一个名为history
"history"： createWebHistory()
"hash"： createWebHashHistory()
"abstract"： createMemoryHistory()
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3.删除 * （捕获所有）路线

现在必须使用带有自定义正则表达式的参数来定义

```
{ path: '/:pathMatch(.*)*', name: 'not-found', component: NotFound },
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

4.命名为空的子路由 path 不附加斜线了

```
const routes = [
  {
    path: '/dashboard',
    name: 'dashboard-parent',
    component: DashboardParent,
    children: [
      { path: '', name: 'dashboard', component: DashboardDefault },
      {
        path: 'settings',
        name: 'dashboard-settings',
        component: DashboardSettings,
      },
    ],
  },
]
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

5.动态的添加删除路由

```
-动态路由主要通过两个函数实现：router.addRoute()和router.removeRoute()
router.addRoute({ path: '/about', component: About })
router.addRoute({ path: '/other', name: 'about', component: Other })
-添加嵌套路由
router.addRoute({ name: 'admin', path: '/admin', component: Admin })
router.addRoute('admin', { path: 'settings', component: AdminSettings })
 嵌套路由相当于
router.addRoute({
  name: 'admin',
  path: '/admin',
  component: Admin,
  children: [{ path: 'settings', component: AdminSettings }],
})
-查看现有路由
router.hasRoute()检查路由是否存在
router.getRoutes()获取包含所有路线记录的数组
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



**二、VueX**

Vuex4 API 与 Vuex3 几乎保持不变，一下是一些重大的改变

1.安装过程

> 要创建新的商店，现在鼓励用户使用新引进的createStore函数

```
import { createStore } from 'vuex'

export const store = createStore({
  state () {
    return {
      count: 1
    }
  }
})
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 要将Vuex安装到vue实例，请传递store代替Vuex

```
import { createApp } from 'vue'
import { store } from './store'
import App from './App.vue'

const app = createApp(App)

app.use(store)

app.mount('#app')
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2.新的功能

> 引入了一个新的 API 来与 Composition API 中的 store 进行交互。您可以使用`useStore`组合函数来检索组件`setup`挂钩内的存储

```
import { useStore } from 'vuex'

export default {
  setup () {
    const store = useStore()
  }
}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)