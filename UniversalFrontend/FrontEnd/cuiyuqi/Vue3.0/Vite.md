 **一. 什么是Vite**

是一种新型的前端构建工具,最初是配合 Vue3.0 一起使用的，

后来适配了各种前端项目

**`vite` 是一个基于 `Vue3`单文件组件的非打包开发服务器**

针对`Vue`单页面组件的无打包开发服务器，可以直接在浏览器运行请求的`vue`文件

作用及优点：

​    快速的冷启动

​    即时的模块热更新

​    真正的按需编译

​    本地开发时热加载编译极快，在大型项目中体验较好。

​    

**二、实现原理** 

- `Vite`在浏览器端使用的是 export import 方式导入和导出的模块；
- `vite`同时实现了按需加载；
- `Vite`高度依赖module script特性。



三、vite 使用方式

  1.vite项目是基于create-vite-app脚手架搭建的，这里我们直接使用npm init命令

```
npm init <脚手架名> <项目名>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2.npm init命令在执行时，如果对应`<脚手架>`的脚手架没有安装的话，就会自动安装对应的脚手架工具

```
npm i create-<脚手架名>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3.所以这里直接执行

```
npm init vite-app <项目名>
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

完整的执行命令

```
npm init vite-app <项目名>
cd <项目名>
npm i 
npm run dev
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



![img](https://img-blog.csdnimg.cn/20210617173349367.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](https://img-blog.csdnimg.cn/20210617173502612.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

![img](https://img-blog.csdnimg.cn/20210617173551763.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)