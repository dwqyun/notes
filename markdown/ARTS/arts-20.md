# ARTS第二十周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

```js
var singleNumber = function (nums) {
  let res = 0;
  for (const num of nums) {

    res = res ^ num;
  }
  return res;
};
```

## Review

[Know your JavaScript data structures - LogRocket Blog](https://blog.logrocket.com/know-your-javascript-data-structures/)

## Tip

- 根据兄弟元素数量设置样式，:nth-child|:nth-of-type()结合~选择器，:only-child等于:first-child:last-child，:only-of-type类同。
- ::selection高亮选择器用于修改颜色属性

## Share

[【第1892期】GPU加速在前端的应用](https://mp.weixin.qq.com/s/T8g8uSn6K_5gz2DiPBWk9Q)
