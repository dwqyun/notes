# ARTS第二十八周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[递归乘法](https://leetcode-cn.com/problems/recursive-mulitply-lcci/)

```js
// 递归乘法。 写一个递归函数，不使用 * 运算符， 实现两个正整数的相乘
/**
 * @param {number} A
 * @param {number} B
 * @return {number}
 */
var multiply = function (A, B) {
  /* 二进制按位相乘 不断移位递归，直到乘数变为0 */
  if (B === 0) return 0;
  return (multiply(A, B >> 1) << 1) + ((B & 1) == 1 ? A : 0);
};
```

## Review

[10 security tips for frontend developers](https://hackernoon.com/10-security-tips-for-frontend-developers-oi4624ld)

## Tip

- `display: none;`和`visibility: hidden;`的区别，使用visibility隐藏后元素仍占空间，display不占；visibility可以使用transition做显示隐藏过度，display不能；visibility隐藏只触发重绘，display则触发重绘和回流；visibility有继承性，父元素使用visibility隐藏后子元素扔可以使用`visibility: visible;`显示，display隐藏节点及其后代都不可见。
- 使用mask遮罩优化PNG图片大小，如带透明边角的PNG图片转换为JPG显示，透明区域单独使用PNG格式后Base64化，赋值mask-image属性，以遮罩JPG边角显示。

## Share

[【第1940期】2020前端性能优化清单之六](https://mp.weixin.qq.com/s/GHUMw2RFK-sXklJTPqoMdg)
