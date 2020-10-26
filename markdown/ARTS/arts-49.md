# ARTS第四十九周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[1～n 整数中 1 出现的次数](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)

```js
/* 1～n 整数中 1 出现的次数
输入一个整数 n ，求1～n这n个整数的十进制表示中1出现的次数。

例如，输入12，1～12这些整数中包含1 的数字有1、10、11和12，1一共出现了5次。
示例 1：
输入：n = 12
输出：5
示例 2：
输入：n = 13
输出：6

限制：
1 <= n < 2^31 */
/**
 * @param {number} n
 * @return {number}
 */
var countDigitOne = function(n) {
  let digit = 1, res = 0;
  let high = Math.floor(n / 10), cur = n % 10, low = 0;
  while (high !== 0 || cur !== 0) {
    if (cur === 0) {
      // 当cur=0 时：此位 1 的出现次数只由高位 high 决定
      res += high * digit;
    } else if (cur === 1) {
      // 当cur=1 时：此位 1 的出现次数由高位 high 和低位 low 决
      res += high * digit + low + 1;
    } else {
      // 当cur=2,3,⋯,9 时：此位 1 的出现次数只由高位 high 决定
      res += (high + 1) * digit;
    }
    low += cur * digit;
    cur = high % 10;
    high = Math.floor(high / 10);
    digit *= 10;
  }
  return res
};
```

## Review

[My Favorite JavaScript Tips and Tricks](https://blog.greenroots.info/my-favorite-javascript-tips-and-tricks-ckd60i4cq011em8s16uobcelc)

## Tip

- 记录使用swiper5(swiper6可使用vue3)实现vue router[命名视图](https://router.vuejs.org/zh/guide/essentials/named-views.html)的卡片页coverflow切换效果，效果类似QQ、网易云的VIP特权介绍；根据特权列表渲染slide下由动态插槽名slot插入的不同命名router-view组件，监听路由parmas参数ID变化，计算activeIndex卡片显示索引，swiper-card组件内监听props activeIndex值变化调用`mySwiper.slideTo(index)`切换卡片；若在swipe-card实现一个subTab切换栏emit事件改变父组件APP.vue activeIndex值即可，若滑动卡片组件触发activeIndex变化，subTab需要监听activeIndex以切换激活项，可使用`activeTabElement.scrollIntoView()({inline: "center"})`水平滚动居中，激活项若显示下划线过渡动画可待activeTabElement滚动后取其`offsetLeft`改变下划线的`left`值；卡片页面内若需要纵向滚动需要限定swiper-slide节点的子元素样式设置`height:100%;overflow-y: scroll;`，横向滚动和卡片滑动touch事件冲突需要单独判断当前触摸对象是否是可横向滑动的节点设定`mySwiper.allowTouchMove = false;`限定swiper不可滑动，则卡片内可以局部横向滑动某一元素内容

```html
<!-- swiper-card.vue -->
<template>
  <div class="swiper-container">
    <div class="swiper-wrapper">
      <div class="swiper-slide" v-for="(item, index) in routerList" :key="item.id">
        <slot :name="item.name" v-bind:item="router">
          {{ router.name }}
        </slot>
      </div>
    </div>
  </div>
</template>

<!-- App.vue activeIndex控制 subTab和swiper-card中slideTo方法 -->
<swiper-card :list="routerList" :activeIndex="activeIndex" @slide-change="">
  <template v-for="(item, index) in routerList" v-slot:[item.name]>
    <router-view :name="item.name"></router-view>
  </template>
</swiper-card>
```

```js
/* swiper-card.vue中处理swiper的初始和销毁 */
const mySwiper = new Swiper('.swiper-container', {
  effect : 'coverflow',
  slidesPerView: 1,
  spaceBetween : 16,
  centeredSlides: true,
  // 是否允许触摸滑动
  allowTouchMove: true,
  // 过渡时将无法滑动
  preventInteractionOnTransition: true,
  coverflowEffect: {
    initialSlide: 0,
    rotate: 0,
    stretch: 10,
    depth: 60,
    modifier: 2,
    slideShadows : true
  },
  on: {
    touchStart: (event) =>{
      // event.currentTarget为swiper节点 可通过class或data属性提前设定哪一控件可以在卡片内横向滑动 如class = sidewise-scrolling
      const scrollingTarget = event.currentTarget.querySelector('swiper-slide-active .sidewise-scrolling');
      // 当前触摸对象是否包含在横向滚动块元素(sidewise-scrolling)n内
      const isContainsTarget = scrollingTarget.contains(event.target);
      // 可再判定滚动块元素是否可滑动 若swiper滑动方向direction为vertical 卡片内需要局部纵向滚动则判断scrollHeight和offsetHeight
      const isScrollable = scrollingTarget.scrollWidth > scrollingTarget.offsetWidth;
      // 设定swiper是否可滑动
      mySwiper.allowTouchMove = !(isContainsTarget && isScrollable);
    },
  },
  slideChange: () =>{
    this.$emit('slide-change', mySwiper.activeIndex);
  },
});

// router配置 命名视图可以在界面中拥有多个单独命名的视图，(同级) 展示多个视图，如果 router-view 没有设置名字，那么默认为 default
const router = new VueRouter({
  routes: [
    {
      path: '/:name/:id',
      name: 'index',
      components: {
        default: '',
        a: () => import('./componentA'),
        b: () => import('./componentB')
      }
    }
  ]
})
```

## Share

[理解ECMAScript规范（三）](https://mp.weixin.qq.com/s/WpsMJe7rPkjFpyF1eKiouA)
