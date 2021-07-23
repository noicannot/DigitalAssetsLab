> ```
> 这篇主要说
> 组合APi的本质composition Api 和 Option Api
> 对于setup 的解释
> 对于 reactive 的详解
> 对于 ref 的详解
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

> 组合Api 就是将封装好的 具备独立的函数组合在一起
>
> \1. composition Api 和 Option Api的混合使用
>
> 2.composition Api 的本质 （混合Api/注入Api）
>
> 3.setup 执行时机
>
> 4.setup 注意点

\1. composition Api 和 Option Api的混合使用 （可以一起混合使用的）

![img](https://img-blog.csdnimg.cn/20210622101641947.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2.composition Api 的本质 （混合Api/注入Api） 知道是这样就行



![img](https://img-blog.csdnimg.cn/20210622102244459.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



\3. setup执行时机

> 实在create和beforecreate 两个生命周期之间使用
>
> beforeCreate 表示组件刚被创建出来，组件data和methods还没初始化好
>
> created 表示组件刚刚被创建出来，并且组建的data和methods已经初始化好
>
>   所以说明 setup 在这两者之间调用 data和methods 没有创建好 所以说不能再data和methods里面使用

setup注意点

> \- 由于在执行setup函数的时候，还未执行created生命周期的方法
>
> 所以setup函数中，是无法使用data和methods的
>
> -由于我们不能这样，所以vue为了避免我们错误使用，他直接将setup函数中的this修改成了undefined
>
> -setup函数只能是同步的不能是异步的

4.什么是reactive

> -reactive 是vue3中提供的实现响应式数据的方法
>
> -在vue2中响应式数据是通过defineProperty来实现
>
> 在vue3中响应式数据是通过es6的proxy来实现

reactive使用的注意点

> -reactive参数必须是对象（json/arr） 
>
> -如果给reactive 传递了其他对象
>
>    +默认情况下修改对象，界面不会自动更新
>
>    +如果想更新，可以通过重新赋值的方式

>  vue修改数组 下表是无法触发响应式的，而vue3 都支持

![img](https://img-blog.csdnimg.cn/20210622113229769.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl81ODQzNzMxMA==,size_16,color_FFFFFF,t_70)

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

5.什么是ref

> ref 和 reactive 一样，也是用来实现响应式数据的方法
>
> 由于 reactive 必须也传递一个对象，所以导致在企业开发中
>
> 如果我们只想让某个变量实现响应式的时候会非常的麻烦
>
> 所以vue3就给我们提供了ref方法，便于对简单值的监听 

 ref的本质

> ref底层的本质还是reactive
>
> 系统会自动根据我们给ref传入的值将他转换
>
> ref(xx)-> reactive({value:xx})

ref注意点

> 在vue中使用ref的值不通过value获取
>
> 在js中使用ref的值必须通过value获取 
