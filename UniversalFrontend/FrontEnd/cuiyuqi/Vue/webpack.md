# webpack
 一、**什么是webpack**

```
webpack`是一个现代 JavaScript 应用程序的`静态模块打包器`(module bundler)，当 webpack 处理应用程序时，它会递归地构建一个`依赖关系图`(dependency graph)，其中包含应用程序需要的每个`模块`，然后将所有这些模块打包成一个或多个 `bundle
```

2.**在`webpack`应用中有两个核心作用**: 

- `模块转换器`，用于把模块原内容按照需求转换成新内容，可以加载非 JS 模块；
- `扩展插件`，在 Webpack 构建流程中的特定时机注入扩展逻辑来改变构建结果或做你想要的事情。

 **二、如何使用**

1.创建一个目录并在终端中进入当前目录执行

```
npm init -y
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2.安装webpack和webpack-cli

```
npm install webpack webpack-cli --save-dev
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3.打开webpack.config.js文件，定义入口和输出 红框的是手动添加

![img](https://img-blog.csdnimg.cn/20210617181748645.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

4.在package.json里面 一个npm脚本，这样运行本地的webpack比较方便

![img](https://img-blog.csdnimg.cn/20210617182046973.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

5.执行

```
npm run build
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

就可以在dist文件夹下生成打包后的bundle.js文件

![img](https://img-blog.csdnimg.cn/20210617182327451.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

三、如果想要处理js以外的文件

就要安装其他的插件

**比如说**

处理样式文件

```
npm install css-loader style-loader --save-dev
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

在webpack.config.js配置文件中配置loader

![img](https://img-blog.csdnimg.cn/20210617182935122.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```
moudle:{
        rules:[
            {
                test:/\.css$/,
                use:['style-loader','css-loader']
            }
        ]
    }
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)