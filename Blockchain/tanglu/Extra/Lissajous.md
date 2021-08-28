package main

import (//调取以下包
	"fmt"
	"image"
	"image/color"
	"image/gif"
	"io"
	"log"
	"math"
	"math/rand"
	"net/http"
	"os"
	"time"
)
var palette=[]color.Color{color.White,color.Black}//颜色设置为黑白
const(
	whiteIndex=0//画板中的第一种颜色
	blackIndex=1//画板中的下一种颜色
)
func main(){//这里的main作用是程序入口
	rand.Seed(time.Now().UTC().UnixNano())//微秒;rand.Seed伪随机函数
	if len(os.Args)>1 && os.Args[1] =="web"{//如果字符串数组长度大于一且第一个字符串为web
		handler := func(w http.ResponseWriter, r *http.Request){//w,r是变量；后边http.ResponseWriter是类型
			lissajous(w)//写入利萨茹图形
		}
		http.HandleFunc("/",handler)
		log.Fatal(http.ListenAndServe("localhost:8000",nil))//启动服务器监听进入8000端口处的请求，log.Fatal是将错误信息进行日志输出的情况
		return
	}
	lissajous(os.Stdout)//标准输出
	fmt.Println(&os.Stdout)//输出标准输出的指针

}
func lissajous(out io.Writer){
	const(
		cycles   =5      //完整的x振荡器变化的个数
		res      =0.001  //角度分辨率
		size     =100    //图像画布包含【-size..+size]
		nframes  =64     //动画中的帧数
		delay    =8      //以10ms为单位的帧间延迟
	)
	freq :=rand.Float64()*3.0
	anim :=gif.GIF{LoopCount:nframes}//anim是gif.GIF结构体类型；创建一个结构体LoopCount，其值设置为"nframes";
	phase :=0.0
	for i :=0;i<nframes;i++{//i的短变量值为0，i<nframes时，i加一；
		rect :=image.Rect(0,0,2*size+1,2*size+1)
		img :=image.NewPaletted(rect,palette)//画板
		for t :=0.0;t<cycles*2*math.Pi;t +=res{
			x :=math.Sin(t)
			y :=math.Sin(t*freq+phase)
			img.SetColorIndex(size+int(x*size+0.5),size+int(y*size+0.5),
				blackIndex)
		}
		phase +=0.1
		anim.Delay=append(anim.Delay ,delay)//anim的延迟；
		anim.Image=append(anim.Image,img)//anim的图像；
	}
	gif.EncodeAll(out,&anim)//注意：忽略编码错误
}
