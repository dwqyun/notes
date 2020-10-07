# ARTS第四十四周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

```js
/* 数字序列中某一位的数字
数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

示例 1：

输入：n = 3
输出：3
示例 2：

输入：n = 11
输出：0

限制：

0 <= n < 2^31 */
/**
 * @param {number} n
 * @return {number}
 */
var findNthDigit = function (n) {
  let base = 9;
  let digits = 1;

  // digits: 个位 9*1 十位 9*10 百位9*100 ...
  while (n - base * digits > 0) {
    n -= base * digits;
    base *= 10;
    digits++;
  }

  // digits位数时对应的数字索引
  let index = n % digits;
  if (index === 0) {
    index = digits;
  }
  let number = 1;
  for (let i = 1; i < digits; i++) {
    number *= 10;
  }
  number += (index === digits) ? n / digits - 1 : n / digits;
  for (let i = index; i < digits; i++) {
    number /= 10;
  }
  return Math.floor(number % 10);
};
```

## Review

[A simple explanation of the “for await …of” statement in Node.js](https://www.mikealche.com/software-development/a-simple-explanation-of-the-for-await-of-statement-in-node-js)

## Tip

- SVG textPath可让文字跟随path路径排列，可以使用工具把SVG图形元素转换为path再使用路径排列效果

```html
<!-- 参考 https://www.zhangxinxu.com/wordpress/2020/09/svg-text-around-path/  -->
<svg viewBox="-10 -10 180 168" width="160" height="148">
  <defs><path id="zxxPath2" d="M118,0c-17,0-31.5,13.5-38,28C73.5,13.5,59,0,42,0C19,0,0,19,0,42c0,47,47.5,59.5,80,106
    c30.5-46.5,80-60.5,80-106C160,19,141,0,118,0z"/></defs>
  <text>
    <textPath href="#zxxPath2">⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐</textPath>
  </text>
</svg>
```

- 对连续英文字符的换行，`word-break: break-all`(允许任意非CJK文本换行)和`word-warp:break-word`(能换行则换行)都不能精确单词换行，可以使用HTML标签`<wbr>`，表示有机会就智能断行，非连续英文字符需要配合`white-space:nowra`不显示换行才有效果

```html
<!-- 参考 https://www.zhangxinxu.com/wordpress/2018/09/html-wbr-word-break/ -->
<div style="width:150px; background:#cd0000;">
  Canvas<wbr>Rendering<wbr>Context2D<wbr>.global<wbr>Composite<wbr>Operation
</div>
```

```js
/* URL地址增加<wbr>标签匹配 */
String.prototype.urlWbr = function () {
  return this.replace(/http(?:s)?:\/\/(.*)\//gi, function (matchs, $1) {
    return matchs.replace($1, $1.replace(/(\/|\.)/g, '<wbr>$1'));
  });
};
'本文地址是https://www.zhangxinxu.com/wordpress/2018/09/html-wbr-word-break/'.urlWbr();
```

## Share

[【第2068期】高级程序4：异步函数](https://mp.weixin.qq.com/s/2Sa9eLpNAyn7B0ID_z1rWg)
