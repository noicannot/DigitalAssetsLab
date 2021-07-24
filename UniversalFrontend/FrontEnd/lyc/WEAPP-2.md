# 了解一下小程序代码的构成

1、了解项目的基本组成结构

![img](https://img-blog.csdnimg.cn/20210627180310681.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

① pages 用来存放所有小程序的页面

② utils 用来存放工具性质的模块（例如：格式化时间的自定义模块）

③ app.js 小程序项目的入口文件

④ app.json 小程序项目的全局配置文件

⑤ app.wxss 小程序项目的全局样式文件

⑥ project.config.json 项目的配置文件

⑦ sitemap.json 用来配置小程序及其页面是否允许被微信索引

2、小程序页面的组成部分

小程序官方建议把所有小程序的页面，都存放在 pages 目录中，以单独的文件夹存在，如图所示：

![img](https://img-blog.csdnimg.cn/20210627180448163.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

其中，每个页面由 4 个基本文件组成，它们分别是：

① .js 文件（页面的脚本文件，存放页面的数据、事件处理函数等）

② .json 文件（当前页面的配置文件，配置窗口的外观、表现等）

③ .wxml 文件（页面的模板结构文件）

④ .wxss 文件（当前页面的样式表文件）

1、JSON 配置文件的作用

JSON 是一种数据格式，在实际开发中，JSON 总是以配置文件的形式出现。小程序项目中也不例外：通过不同的 .json 配置文件，可以对小程序项目进行不同级别的配置。

小程序项目中有 4 种 json 配置文件，分别是：

① 项目根目录中的 app.json 配置文件

② 项目根目录中的 project.config.json 配置文件

③ 项目根目录中的 sitemap.json 配置文件

④ 每个页面文件夹中的 .json 配置文件

\2. app.json 文件

app.json 是当前小程序的全局配置，包括了小程序的所有页面路径、窗口外观、界面表现、底部 tab 等。 Demo 项目里边的 app.json 配置内容如下：

![img](https://img-blog.csdnimg.cn/20210627180724104.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

简单了解下这 4 个配置项的作用：

① pages：用来记录当前小程序所有页面的路径

② window：全局定义小程序所有页面的背景色、文字颜色等

③ style：全局定义小程序组件所使用的样式版本

④ sitemapLocation：用来指明 sitemap.json 的位置

3、project.config.json 文件

project.config.json 是项目配置文件，用来记录我们对小程序开发工具所做的个性化配置，例如： （1）setting 中保存了编译相关的配置

（2）projectname 中保存的是项目名称

（3）appid 中保存的是小程序的账号 ID

\4. sitemap.json 文件

微信现已开放小程序内搜索，效果类似于 PC 网页的 SEO。sitemap.json 文件用来配置小程序页面是否允许微信索引。 当开发者允许微信索引时，微信会通过爬虫的形式，为小程序的页面内容建立索引。当用户的搜索关键字和页面的索引匹配成功的时候，小程序的页面将可能展示在搜索结果中。

![img](https://img-blog.csdnimg.cn/20210627180937122.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

注意：sitemap 的索引提示是默认开启的，如需要关闭 sitemap 的索引提示，可在小程序项目配置文件 project.config.json 的 setting 中配置字段 checkSiteMap 为 false

\5. 页面的 .json 配置文件

小程序中的每一个页面，可以使用 .json 文件来对本页面的窗口外观进行配置，页面中的配置项会覆盖 app.json 的 window 中相同的配置项。例如：

![img](https://img-blog.csdnimg.cn/20210627181017341.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

\6. 新建小程序页面

只需要在 app.json -> pages 中新增页面的存放路径，小程序开发者工具即可帮我们自动创建对应的页面文件，如图所示：

![img](https://img-blog.csdnimg.cn/20210627181044235.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

\7. 修改项目首页

只需要调整 app.json -> pages 数组中页面路径的前后顺序，即可修改项目的首页。小程序会把排在第一位的页面，当作项目首页进行渲染，如图所示：

![img](https://img-blog.csdnimg.cn/20210627181111725.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80OTQ4MTE4MA==,size_16,color_FFFFFF,t_70)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

以上就是我们新建小程序生成的目录文件的全部介绍啦~
