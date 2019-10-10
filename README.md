# vue-awesome-swiper(vue-awesome-swiper 的安装和使用)
# 示例

[Demo](https://surmon-china.github.io/vue-awesome-swiper)

[移动端](https://github.com/surmon-china/vue-awesome-swiper/blob/master/examples/44-mobile-fullpage-example.vue)


# 使用方法

``` bash
npm install vue-awesome-swiper --save
```
## 全局引入
``` javascript
import VueAwesomeSwiper from 'vue-awesome-swiper'
import 'swiper/dist/css/swiper.css'//这里注意具体看使用的版本是否需要引入样式，以及具体位置。
Vue.use(VueAwesomeSwiper, /* { default global options } */)
```
## 组件方式引用
```html
<swiper :options="swiperOption">
    <swiper-slide><img src="static/images/jay.jpg"></swiper-slide>
    <swiper-slide><img src="static/images/jay.jpg"></swiper-slide>
    <swiper-slide><img src="static/images/jay.jpg"></swiper-slide>
    <swiper-slide><img src="static/images/jay.jpg"></swiper-slide>
    <swiper-slide><img src="static/images/jay.jpg"></swiper-slide>
    <swiper-slide><img src="static/images/jay.jpg"></swiper-slide>
</swiper>
 <!--以下看需要添加-->
<div class="swiper-scrollbar"></div> //滚动条
<div class="swiper-button-next"></div> //下一项
<div class="swiper-button-prev"></div> //上一项
<div class="swiper-pagination"></div> //标页码
```
```js
import 'swiper/dist/css/swiper.css'////这里注意具体看使用的版本是否需要引入样式，以及具体位置。
import { swiper, swiperSlide } from 'vue-awesome-swiper'
data() {
    return {
      swiperOption: {
        notNextTick: true,
        autoplay: true,
        speed: 1000,
        loop: true
      },
    };
  },
 components: {   //
    swiper,
    swiperSlide
  },
```
## 用vue-awesome-swiper实现轮播图, 点击事件不生效
在最新的swiper中，swiper绑定的事件中，是通过this指向当前swiper对象的。而在事件回调中，我们需要获取vue页面data中的数据。但是此时的this并不指向vue对象。

解决:

html
```html
<swiper :options="swiperOption" ref="mySwiper">
    <swiper-slide v-if="imgList.length>0" v-for="(item,index) in imgList" :key='index'>
        <img :src="item.imgurl">
    </swiper-slide>
</swiper>
```
js
```js
data() {
    return {
      swiperOption: {
        notNextTick: true,
        autoplay: 3000,
        direction: 'horizontal',
        grabCursor: true,
        setWrapperSize: true,
        autoHeight: true,
        paginationClickable: true,
        mousewheelControl: true,
        observeParents: true,
        loop: true,
        on:{
          // 使用es6的箭头函数，使this指向vue对象
          click: ()=>{
            // 通过$refs获取对应的swiper对象
            let swiper = this.$refs.mySwiper.swiper;
            let i = swiper.activeIndex;
            let flag = this.imgList[i];
            location.href = flag.url;
          }
        }
    }
}
```
```html
autoplay:

 autoplay: {
 delay: 3000, //自动切换的时间间隔，单位ms
 stopOnLastSlide: false, //当切换到最后一个slide时停止自动切换
 stopOnLastSlide: true, //如果设置为true，当切换到最后一个slide时停止自动切换。
 disableOnInteraction: true, //用户操作swiper之后，是否禁止autoplay。
 reverseDirection: true, //开启反向自动轮播。
 waitForTransition: true, //等待过渡完毕。自动切换会在slide过渡完毕后才开始计时。 
},
fade:

 fadeEffect: {
 crossFade: false,
 }
cube:

 cubeEffect: {
 slideShadows: true, //开启slide阴影。默认 true。
 shadow: true, //开启投影。默认 true。
 shadowOffset: 100, //投影距离。默认 20，单位px。
 shadowScale: 0.6 //投影缩放比例。默认0.94。
 },
coverflow:

 coverflowEffect: {
 rotate: 30, //slide做3d旋转时Y轴的旋转角度。默认50。
 stretch: 10, //每个slide之间的拉伸值，越大slide靠得越紧。 默认0。
 depth: 60, //slide的位置深度。值越大z轴距离越远，看起来越小。 默认100。
 modifier: 2, //depth和rotate和stretch的倍率，相当于depth*modifier、rotate*modifier、stretch*modifier，值越大这三个参数的效果越明显。默认1。
 slideShadows : true //开启slide阴影。默认 true。
 },
flip:

 flipEffect: {
 slideShadows : true, //slides的阴影。默认true。
 limitRotation : true, //限制最大旋转角度为180度，默认true。
 }
zoom:

 zoom: {
 maxRatio: 5, //最大倍数
 minRatio: 2, //最小倍数
 toggle: false, //不允许双击缩放，只允许手机端触摸缩放。
 containerClass: 'my-zoom-container', //zoom container 类名
 },
navigation:

 navigation: {
 nextEl: '.swiper-button-next', //前进按钮的css选择器或HTML元素。
 prevEl: '.swiper-button-prev', //后退按钮的css选择器或HTML元素。
 hideOnClick: true, //点击slide时显示/隐藏按钮
 disabledClass: 'my-button-disabled', //前进后退按钮不可用时的类名。
 hiddenClass: 'my-button-hidden', //按钮隐藏时的Class
 },
pagination:

 pagination: {
 el: '.swiper-pagination',
 type: 'bullets',
 //type: 'fraction',
 //type : 'progressbar',
 //type : 'custom',
 progressbarOpposite: true, //使进度条分页器与Swiper的direction参数相反
 bulletElement : 'li', //设定分页器指示器（小点）的HTML标签。
 dynamicBullets: true, //动态分页器，当你的slide很多时，开启后，分页器小点的数量会部分隐藏。
 dynamicMainBullets: 2, //动态分页器的主指示点的数量
 hideOnClick: true, //默认分页器会一直显示。这个选项设置为true时点击Swiper会隐藏/显示分页器。
 clickable: true, //此参数设置为true时，点击分页器的指示点分页器会控制Swiper切换。
},
Scrollbar:

 scrollbar: {el: '.swiper-scrollbar', hide: true, //滚动条是否自动隐藏。默认：false，不会自动隐藏。
 draggable: true, //该参数设置为true时允许拖动滚动条。
 snapOnRelease: true, //如果设置为false，释放滚动条时slide不会自动贴合。
 dragSize: 30, //设置滚动条指示的尺寸。默认'auto': 自动，或者设置num(px)。
 }
```
