# ARTS第十八周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[2的幂](https://leetcode-cn.com/problems/power-of-two/)

```js
/**
 * @param {number} n
 * @return {boolean}
 */
var isPowerOfTwo = function (n) {
  let temp = n;
  while (1) {
    if (temp === 1) {
      return 1;
    }

    if (temp % 2 !== 0 || temp === 0) {
      return 0;
    }

    temp = temp / 2;
  }
};
```

## Review

[How to Hide/Reveal a Sticky Header on Scroll (With JavaScript)](https://webdesign.tutsplus.com/tutorials/how-to-hide-reveal-a-sticky-header-on-scroll-with-javascript--cms-33756)

## Tip

- paste剪切板粘贴事件处理clipboardData可实现输入框粘贴上传图片操作，监听copy事件可通过clipboardData.setData定义剪贴板内容。
- sass-loader使用时，若scss文件需要使用"url rewriting"功能需要引入resolve-urloader,解决图片等资源引入问题。
- 在使用drop-shadow阴影+透明边框显示变色图标时，由于层级影响overflow:hidden；失效导致图标不显示，需要使用transform:translateZ(0);启用GPU合成，也可改变z-index但开销比合成大。
- Chrome可以在chrome://flags中开启dark模式，会自动反转颜色适配深色，可以使用媒体查询(prefers-color-scheme: dark)自定义适配dark。

## Share

[【第1870期】巧妙实现带圆角的渐变边框](https://mp.weixin.qq.com/s/Fs7rpplWU8at7Y7w1No9JQ)
