1.Elemnet UI

![img](https://img-blog.csdnimg.cn/20210630093533991.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 推出Element Plus

```
源码地址 https://github.com/element-plus/element-plus
官方网站 https://element-plus.org
国内加速镜像 https://element-plus.gitee.io
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

vue3.0如何使用

首先你要创建vue3.0的项目

初始化vite项目

```
npm init @vitejs/app my-vue-app --template vue
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

1>.引入Element Plus UI 组件库（以下是vite工程的使用）

首先安装

```
npm i element-plus
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 然后修改项目入口文件，引入 Element Plus 库和相关样式文件

```
import { createApp } from 'vue'
import App from './App.vue'
import ElementPlus from 'element-plus'
import 'element-plus/lib/theme-chalk/index.css'
createApp(App).use(ElementPlus).mount('#app')
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

 重新启动项目，就可以愉快的使用 `Element Plus` 了

2.Vant

> Vant 是针对移动端的 UI 组件库，在他们的 Github 上同样找到了升级到 Vue 3 的声明。如果要开发移动端项目，Vant 是个不错的选择。

![img](https://img-blog.csdnimg.cn/2021063009384023.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> - 源码地址 https://github.com/youzan/vant
> - 官方网站 https://youzan.github.io/vant/#/zh-CN/

 3.Vuetify

> 到2021年末 可推出使用vue3.0 使用的版本