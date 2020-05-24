# ARTS第十一周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[反转字符串](https://leetcode-cn.com/problems/reverse-string/)

```js
/**
 * @param {character[]} s
 * @return {void} Do not return anything, modify s in-place instead.
 */
var reverseString = function(s) {
  if (!Array.isArray(s)) {
    return;
  }

  const len = s.length;
  for (let i = 0; i < len / 2; i++) {
    const temp = s[i];
    s[i] = s[len - 1 - i];
    s[len - 1 - i] = temp;
  }
  return s;
};
```

## Review

[infinity-in-javascript](https://dmitripavlutin.com/infinity-in-javascript/)

## Tip

- canvas的measureText可以计算预置样式文本的宽度大小，可应用于文本截断。
- 使用quill可以直接操作DOM更新Delta数据且更新界面
- scss选择器属性键和值都可以使用占位符传递变量

## Share

[【第1748期】前端工程师的产品思维](https://mp.weixin.qq.com/s/XD07GPyMXDXNqdHu--3hAA)
