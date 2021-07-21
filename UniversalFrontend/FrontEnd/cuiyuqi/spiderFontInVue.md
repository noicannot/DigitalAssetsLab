1.可以先建一个文件夹 里面包括

![里面包括](https://img-blog.csdnimg.cn/20210528152126305.png)

2.1>.css文件夹->index.css     2>.font(里面放的是ttf字体包)  3>.index.html 引入 4>.没有 .font-spider文件夹 这个是安装字蛛完才显示

![img](https://img-blog.csdnimg.cn/20210528153442503.png)

3.css里面需要引入字体

```
@font-face {

  font-family: "AlibabaPuHuiTi-Medium, AlibabaPuHuiTi";

  src: url("../font/Alibaba-PuHuiTi-Medium.ttf") format('truetype');

  font-weight: normal;

  font-style: normal;

}
```

 4.html里引入

![img](https://img-blog.csdnimg.cn/20210528160918758.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

5.安装 字蛛 

```
npm install font-spider -g
```


 安装完成产看版本号

```
font-spider --version
```

 6. 出现一个 .spider-font 文件夹 这里面是原来的字体包
