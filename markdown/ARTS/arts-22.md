# ARTS第二十二周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[整数反转](https://leetcode-cn.com/problems/reverse-integer/)

```js
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function (x) {
  const MAX_INTEGER = Math.pow(2, 31);
  const num = parseInt(x.toString().split('').reverse().join(''));

  if (num > MAX_INTEGER) {
    return 0;
  }
  return x < 0 ? -num : num;
};
```

## Review

[How To Write Fast, Memory-Efficient JavaScript — Smashing Magazine](https://www.smashingmagazine.com/2012/11/writing-fast-memory-efficient-javascript/)

## Tip

- 尽量使用transform和opacity属性实现动画效果，它们可以避免layout和paint，同时可以使用will-change:transform;|will-change:opacity;提升元素层，或者transform: translateZ(0);以实现GPU加速，但需要适当的在限制选择器上使用。
- requestAnimationFrame可以使用在频繁修改样式如scroll时的多次触发上，减少layout和paint；批量修改DOM，需要display:none;和克隆节点替换以及使用临时变量缓存不变的DOM尺寸值。

## Share

[十分钟了解git那些“不常用”命令](https://mp.weixin.qq.com/s/WsmF5DrMQAoXKBhx4GoK1A)
