>  **目录**
>
> [什么是微前端](#什么是微前端)
>
> [Systemjs 模块化解决方案](#Systemjs 模块化解决方案)
>
> [Single-spa 微前端框架实战](#Single-spa 微前端框架爱实战)
>
> [基于 Module Federation 的微前端架构](#基于 Module Federation 的微前端架构)
>
> ------
>
> ### [什么是微前端](#什么是微前端)
>
> npm 包的几个注意点 
>
> > -使用前端项目 还是以npm 包为主的 发布的效率是不高的 如果需要迭代 npm 包里面的一些业务逻辑 需要发布这个包之后 每一个使用这个模块都需要更新一次（这是对内的）
> >
> > 对外也是一样的 用户拿到之后也是需要更新的 还需要在内部更新发布
> >
> > 那把公用的部分做成 npm包的形式 效率也是非常高的
> >
> > -多团队使用的话也不方便 如果一个人做的包是一个形式 另一个也是另一种风格
> >
> > 那么 做大项目就很难了
>
> 微前端
>
> > **----微前端**只是管理这种复杂性的一种方法，通过将产品拆分为更小、更简单的应用程序，这些应用程序可以由独立的自治团队一直交付到生产环境。
> >
> > ----微前端是从微服务的概念借鉴而来
> >
> > ----把整个 前端的一个大的整体分解成小而简单的块，那么这些块可以去单独的开发 部署
> >
> > ​    同时仍然可以将这些块聚合到一起 成为产品 到客户面前去展示
> >
> > ----多个可独立交付的小型前端应用 聚合在一个整体应用的一种架构风格
> >
> > ----这种思想 模块 风格就是微前端
>
> 微前端解决了哪些问题
>
> > 项目太多太杂 
> >
> > 项目时间很久 运用了各种技术 要整合到一起
> >
> > 升级更新新的功能非常的繁琐
> >
> > 把之前的旧项目 直接放到微前端里面 进行开发
> >
> > 微前端本身不是一门技术 整合了策略方法思维的这种方法的架构模型
>
> 什么项目适合 微前端架构
>
> > 拆分巨型项目使项目变得更加容易维护
> >
> > 兼容历史应用 实现增量开发
>
> 微前端架构的特点
>
> > 独立部署 增量迁移 团队自治 松耦合代码
>
> 微前端架构方案
>
> > 自由组织模式 基座模式（必须有一个大的容器 应用最多的） 去中心模式（脱离这种模式）
>
> [Systemjs 模块化解决方案](#Systemjs 模块化解决方案) 
>
>  对兼容性不好 版本要求很高
>
> webpack的配置文件
>
> ![img](https://img-blog.csdnimg.cn/20210709114747496.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 
>
> ![img](https://img-blog.csdnimg.cn/20210709114804646.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> [Single-spa 微前端框架实战](#Single-spa 微前端框架爱实战)
>
> 是什么
>
> > 官网地址：https://single-spa.js.org/ 是一个实现微前端的架构框架
>
> 在single-spa框架中有三种类型的微前端应用：
>
> 创建容器去接纳
>
> 1.single-spa-application/parcel :微前端架构框架中的微应用，可以使用vue,react,angulard等框架
>
> 2.single-spa root config:创建微前端容器应用
>
> 3.utility modules:公共模块应用，菲渲染组件，用于跨应用共享javascript逻辑的微应用
>
> 创建
>
> 1.安装 ：
>
> ```
> npx create-single-spa --moduleType root-config
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> ![img](https://img-blog.csdnimg.cn/20210709165252506.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 
>
> 1. 创建后，导航到新创建的应用程序文件夹
> 2. `start`使用您首选的包管理器运行脚本
>
> 
>
> ```
> 注册应用程序#
> 返回 root-config 并将您的应用程序添加到导入映射中 src/index.ejs
> 
> 推荐应用的 package.json name 字段
> 注册为单一水疗应用程序
> 
> 如果不使用 single-spa 布局引擎
> 
> 打开 src/root-config.js
> 删除注册@single-spa/welcome为应用程序的代码
> 取消注释示例registerApplication代码并使用应用程序的模块名称更新它
> 如果使用 single-spa 布局引擎
> 
> 删除现有<application name="@single-spa/welcome"></application>元素
> <application name=""></application>使用name上一步中导入映射中使用的模块名称添加您自己的元素
> 就是这样！您的第一个单水疗应用程序现在应该在您的根配置中运行。
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 运行
>
> ```
> create-single-spa
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 没有全局安装的情况下使用create-single-spa:
>
> ```
> npm init single-spa
> 
> #or
> npx create-single-spa
> 
> #or
> yarn create single-spa
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)