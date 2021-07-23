# 介绍一下小程序的 WXML，WXSS 和 JS 逻辑交互

**一、WXML 模板**

**1. 什么是 WXML**

WXML（WeiXin Markup Language）是小程序框架设计的一套标签语言，用来构建小程序页面的结构，其作用类似于网页开发中的 HTML。

![img](https://img-blog.csdnimg.cn/20210710172057221.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2. WXML 和 HTML 的区别**

① 标签名称不同

HTML （div, span, img, a）

WXML（view, text, image, navigator）

② 属性节点不同

<a href="#">超链接</a>

<navigator url="/pages/home/home"></navigator>

③ 提供了类似于 Vue 中的模板语法

数据绑定 列表渲染 条件渲染

**二、WXSS 样式**

**1. 什么是 WXSS**

WXSS (WeiXin Style Sheets)是一套样式语言，用于描述 WXML 的组件样式，类似于网页开发中的 CSS

![img](https://img-blog.csdnimg.cn/20210710172353526.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2. WXSS 和 CSS 的区别**

① 新增了 rpx 尺寸单位

CSS 中需要手动进行像素单位换算，例如 rem

WXSS 在底层支持新的尺寸单位 rpx，在不同大小的屏幕上小程序会自动进行换算

② 提供了全局的样式和局部样式

项目根目录中的 app.wxss 会作用于所有小程序页面

局部页面的 .wxss 样式仅对当前页面生效

③ WXSS 仅支持部分 CSS 选择器

.class 和 #id

element

并集选择器、后代选择器

::after 和 ::before 等伪类选择器

**三、JS 逻辑交互**

**1. 小程序中的 .js 文件**

一个项目仅仅提供界面展示是不够的，在小程序中，我们通过 .js 文件来处理用户的操作。例如：响应用户的点击、获取用户的位置等等。

![img](https://img-blog.csdnimg.cn/20210710172538629.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

**2. 小程序中 .js 文件的分类**

小程序中的 JS 文件分为三大类，分别是：

① app.js

​ 是整个小程序项目的入口文件，通过调用 App() 函数来启动整个小程序

② 页面的 .js 文件

​ 是页面的入口文件，通过调用 Page() 函数来创建并运行页面

③ 普通的 .js 文件

​ 是普通的功能模块文件，用来封装公共的函数或属性供页面使用

**以上就是今天所分享的内容啦~**
