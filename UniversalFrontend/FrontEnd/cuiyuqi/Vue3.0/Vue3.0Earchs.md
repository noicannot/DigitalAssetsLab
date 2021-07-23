>  1.安装
>
> ```
> npm install echarts --save
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 2.引入
>
> ```
> import echarts from 'echarts'
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 3.容器
>
> ```
> <div ref="chart" style="width: 600px; height: 400px"></div>
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 4.配置 写入setup
>
> ```
>     const init = () => {
>       var myChart = echarts.init(state.chart);
>       // 指定图表的配置项和数据
>       var option = {
>         title: {
>           text: "ECharts 入门示例",
>         },
>         tooltip: {},
>         legend: {
>           data: ["销量"],
>         },
>         xAxis: {
>           data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],
>         },
>         yAxis: {},
>         series: [
>           {
>             name: "销量",
>             type: "bar",
>             data: [5, 20, 36, 10, 10, 20],
>           },
>         ],
>       };
>       myChart.setOption(option);
>     };
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 5.如有动态的 改变要return出去
>
> ```
>     return { init };
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 6.在生命周期 onmounted 里面调用 如果只是展示不做动态改变可省略第5
>
> ```
>  onMounted(() => {
>       init();
>     });
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)