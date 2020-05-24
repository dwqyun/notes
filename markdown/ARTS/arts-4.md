# ARTS第四周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[字符串转换整数 (atoi)](https://leetcode-cn.com/explore/interview/card/tencent/221/array-and-strings/897/)

```js
/**
 * @param {string} str
 * @return {number}
 */
var myAtoi = function(str) {
  let s = str.trim();
  if (!s.length) {
    return 0;
  }
  let isInteger = true;
  let n = 0;
  const M = 2 ** 31;
  const INT_MAX = M - 1
  const INT_MIN = Number('-' + M);
  if (s[0] === '-' && Number(s[1])) {
    isInteger = false;
    n = parseInt(s.replace('-', ''), 10) || 0;
  }
  else {
    n = parseInt(s, 10) || 0;
  }

  if (n > INT_MAX && isInteger) {
    return INT_MAX;
  } else if (n > M && !isInteger) {
    return INT_MIN;
  } else {
    return isInteger ? n : -n;
  }
};
```

## Review

[Various Methods for Expanding a Box While Preserving the Border Radius](https://css-tricks.com/various-methods-for-expanding-a-box-while-preserving-the-border-radius/)

- 使用伪元素、伪类、绝对定位偏移大小组合transition生成盒子扩展效果
- 结合calc函数改变宽高尺寸大小、边框、内边距、外边距生成盒子扩展效果
- em单位结合font-size：0->1的变化生成盒子扩展效果
- 使用scale、clip-path的inset生成盒子扩展效果

## Tip

- HTMLElement.innerText和Node.textContent，获取对象不同。值获取规则不同，innerText会保留块级元素的换行特性；display:none元素是无法使用innerText获取的，但是textContent却可以；读取innerText属性值会考虑CSS样式将触发回流而textContent只是单纯读取文本内容；IE浏览器不符合上面规则两者表现一致。

> 推荐使用textContent，兼容IE8则需要缺省使用innerText；如要改变DOM元素文字内容，推荐使用textContent，而不是innerHTML，性能会更高一点。

## Share

[【第1719期】简明 JavaScript 函数式编程-入门篇](https://mp.weixin.qq.com/s/PUblSsxKrIAJfGMhBesGsw)
