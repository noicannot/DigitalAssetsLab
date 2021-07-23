>  1.安装swiper
>
> ```
> npm install swiper --save
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 2.引入
>
> ```
> import { onMounted } from "vue";
> import Swiper, {
>   Autoplay,
>   EffectCoverflow,
>   EffectCube,
>   Pagination,
>   Navigation,
> } from "swiper";
> Swiper.use([Autoplay, EffectCoverflow, EffectCube, Pagination, Navigation]);
> // swiper-bundle.min.css 决定了小圆点和左右翻页，如果不需要可以不引用
> import "swiper/swiper-bundle.min.css";
> // swiper.less/sass/css 决定了基础的样式
> import "swiper/swiper.min.css";
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 3.配置项
>
> ```
> export default {
>   setup() {
>     onMounted(() => {
>       new Swiper(".swiper1", {
>         pagination: {
>           el: ".swiper-pagination",
>         },
>         navigation: {
>           nextEl: ".swiper-button-next",
>           prevEl: ".swiper-button-prev",
>           hideOnClick: true,
>         },
>         autoplay: {
>           delay: 3000,
>           stopOnLastSlide: false,
>           disableOnInteraction: false,
>         },
>         on: {
>           navigationShow: function () {
>             console.log("按钮显示了");
>           },
>         },
>       });
> 
>       new Swiper(".swiper2", {
>         //循环
>         loop: true,
>         //每张播放时长3秒，自动播放
>         spaceBetween: 25,
>         effect: "coverflow",
>         grabCursor: true,
>         centeredSlides: true,
>         slidesPerView: 1.32,
>         autoplay: {
>           delay: 3000,
>           stopOnLastSlide: false,
>           disableOnInteraction: false,
>         },
>         coverflowEffect: {
>           rotate: 0,
>           stretch: 0,
>           depth: 100,
>           modifier: 1,
>           slideShadows: true,
>         },
>       });
> 
>       new Swiper(".swiper3", {
>         loop: true,
>         autoplay: {
>           delay: 3000,
>           stopOnLastSlide: false,
>           disableOnInteraction: false,
>         },
>         effect: "cube",
>         cubeEffect: {
>           slideShadows: true,
>           shadow: true,
>           shadowOffset: 100,
>           shadowScale: 0.6,
>         },
>       });
>     });
>   },
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)
>
> 4.template中运用
>
> ```
> <div class="swiper-container swiper1" style="height: 650px">
>         <div class="swiper-wrapper">
>           <div class="swiper-slide">
>             <img src="./assets/img/1.jpeg" alt="" />
>           </div>
>           <div class="swiper-slide">
>             <img src="./assets/img/1.jpeg" alt="" />
>           </div>
>           <div class="swiper-slide">
>             <img src="./assets/img/1.jpeg" alt="" />
>           </div>
>         </div>
>         <!-- 如果需要分页器 -->
>         <div class="swiper-pagination"></div>
> 
>         <div class="swiper-button-prev"></div>
>         <!--左箭头。如果放置在swiper-container外面，需要自定义样式。-->
>         <div class="swiper-button-next"></div>
>         <!--右箭头。如果放置在swiper-container外面，需要自定义样式。-->
>       </div>
> ```
>
> ![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)