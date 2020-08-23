# ARTS第四十一周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[数组中数字出现的次数](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof)

```js
/* 一个整型数组 nums 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。


示例 1：

输入：nums = [4,1,4,6]
输出：[1,6] 或 [6,1]
示例 2：

输入：nums = [1,2,10,4,1,4,3,3]
输出：[2,10] 或 [10,2]


限制：

2 <= nums.length <= 10000 */

/**
 * @param {number[]} nums
 * @return {number[]}
 */
var singleNumbers = function (nums) {
  // 数组元素进行异或得到两个出现一次的数字的异或结果 [4,1,4,6] => 7
  const sum = nums.reduce((preVal, curVal) => preVal ^ curVal);
  // 根据异或结果 找从右向左找1的对应的数 由这一位划分数组 7 => 0111 => [4, 4, 6] + [1]
  let index = 1;
  while ((sum & index) === 0) {
    index = index << 1;
  }

  let res1 = 0;
  let res2 = 0;

  // 两数组再进行异或得到出现一次的数字
  for (const n of nums) {
    if ((n & index) === 0) {
      res1 = res1 ^ n;
    }
    else {
      res2 = res2 ^ n;
    }
  }

  return [res1, res2]
};

```

## Review

[Google Search Operators: The Complete List (42 Advanced Operators)](https://ahrefs.com/blog/google-advanced-search-operators/)

## Tip

- 使用swiper实现图片循环轮播时，如果设备尺寸发生变化应该销毁swiper`mySwiper.destroy(deleteInstance, cleanupStyles)`，再重新绑定轮播列表初始化实例`new Swiper(swiperContainer, parameters)`，避免轮播复制图片(`loopAdditionalSlides`)宽高尺寸未适配屏幕尺寸；图片居中轮播可设置左右的偏移量`slidesOffsetBefore slidesOffsetAfter`；轮播模式下图片的点击事件可以结合`dataset`判断当前点击项

```js
let mySwiper = null;
// 默认配置
const defaultOptions = {};
function initSwiper() {
  // TODO: 配置选项参数初始 根据轮播列表、屏幕尺寸变化
  const options = { ...defaultOptions, ...initSwiperOption() };
  /* 常用配置
    slidesPerView: slider容器同时显示的slides数量
    width: swiper区宽度
    slidesOffsetBefore: slide与左边框的预设偏移量
    slidesOffsetBefore: slide与右边框的预设偏移量
    spaceBetween: slide之间间距
    allowTouchMove: 是否禁止触摸滑动
    loop: true则开启loop模式，会在原本slide前后复制若干个slide
    autoplay: 为true启动自动切换
    pagination: 分页器
    scrollbar: 滚动条
    lazy: 图片延迟加载
    on:{ click: function(){} }: 事件监听
    ...
  */
  if (mySwiper) {
    try {
      mySwiper.destroy();
    } catch (error) {
      console.warn(error);
    }
  }
  else {
    mySwiper = new Swiper('.swiper-container', options);
  }
};
```

- 文本截断除了常用的`text-overflow`  和 `-webkit-line-clamp`实现，还可以使用`float`和伪元素`::after ::before`，移动端大多基于WebKit 内核的浏览器可以使用`-webkit-line-clamp` 属性；[参考css-tricks](https://css-tricks.com/line-clampin/)，还可以使用JS计算处理文本截断，或者使用`canvas measureText`测量指定样式文本，准确实现指定宽度内放入文本加省略号；在适配RTL时除了使用`direction: rtl;`和`transform: scaleX(-1);`改变文本和方向性图片阅读方向，还需要对应置换`left right`属性值，尽量使用`flex`布局；RTL下`-webkit-line-clamp`实现的多行省略失效，省略号未显示，新特性`text-overflow: ellipsis clip;`只支持Firefox暂未找到解决方法

```css

/* 单行文本截断 */
.single-line-ellipsis {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
/* 多行文本截断 */
.multi-line-ellipsis {
  display: -webkit-box;
  overflow: hidden;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}
```

## Share

[【第2028期】What I'm thinking about: JS疲劳、招聘](https://mp.weixin.qq.com/s/42r-HqT8UOvQV-mLgkYHpA)
