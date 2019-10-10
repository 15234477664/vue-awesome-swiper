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
解决:
```html
<swiper :options="swiperOption" ref="mySwiper">
    <swiper-slide v-if="imgList.length>0" v-for="(item,index) in imgList" :key='index'>
        <img :src="item.imgurl">
    </swiper-slide>
</swiper>
```
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
