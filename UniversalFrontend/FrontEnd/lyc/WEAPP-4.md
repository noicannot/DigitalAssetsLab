**小程序的宿主环境**

\*\*小程序的宿主环境——宿主环境简介

1.  什么是宿主环境\*\*

宿主环境（host environment）指的是程序运行所必须的依赖环境。例如： Android 系统和 iOS 系统是两个不同的宿主环境。安卓版的微信 App 是不能在 iOS 环境下运行的，所以，Android 是安卓软件的宿主环境，脱离了宿主环境的软件是没有任何意义的！

![img](https://img-blog.csdnimg.cn/20210717175620566.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](https://img-blog.csdnimg.cn/20210717175802192.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2. 小程序的宿主环境**

手机微信是小程序的宿主环境，如图所示：

![img](https://img-blog.csdnimg.cn/20210717175718670.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

小程序借助宿主环境提供的能力，可以完成许多普通网页无法完成的功能，例如： 微信扫码、微信支付、微信登录、地理定位、etc…

**1. 小程序启动的过程**

① 把小程序的代码包下载到本地

② 解析 app.json 全局配置文件

③ 执行 app.js 小程序入口文件，调用 App() 创建小程序实例

④ 渲染小程序首页

⑤ 小程序启动完成

**2. 页面渲染的过程**

① 加载解析页面的 .json 配置文件

② 加载页面的 .wxml 模板和 .wxss 样式

③ 执行页面的 .js 文件，调用 Page() 创建页面实例

④ 页面渲染完成

**小程序的宿主环境—— 组件**

**1. 小程序中组件的分类**

小程序中的组件也是由宿主环境提供的，开发者可以基于组件快速搭建出漂亮的页面结构。官方把小程序的组件分为了 9 大类，分别是：

① 视图容器

② 基础内容

③ 表单组件

④ 导航组件

⑤ 媒体组件

⑥ map 地图组件

⑦ canvas 画布组件

⑧ 开放能力

⑨ 无障碍访问

**2. 常用的视图容器类组件**

① view 普通视图区域 类似于 HTML 中的 div，是一个块级元素 常用来实现页面的布局效果

② scroll-view 可滚动的视图区域 常用来实现滚动列表效果

③ swiper 和 swiper-item 轮播图容器组件 和 轮播图 item 组件
