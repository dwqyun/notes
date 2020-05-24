# ARTS第十二周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[反转字符串中的单词 III](https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/)

```js
/**
 * @param {string} s
 * @return {string}
 */
var reverseWords = function(s) {
  if (s == '') {
    return '';
  }
  let strArray = s.split(' ');
  for (let i = 0; i < strArray.length; i++) {
    strArray[i] = [...strArray[i]].reverse().join('');
  }
  return strArray.join(' ');
};
```

## Review

[7-tips-to-handle-undefined-in-javascript](https://dmitripavlutin.com/7-tips-to-handle-undefined-in-javascript/)

## Tip

- `delete x`归根到底，是在删除一个表达式的、引用类型的结果（Result），而不是在删除 x 表达式，或者这个删除表达式的值（Value）。
- `var x = y = 100`不是声明语句而是赋值表达式，右边是一个表达式,隐式地声明了一个全局变量y，并赋值为 100，表达式结果是右操作数的值。

## Share

[【第1752期】深入理解 JavaScript 原型](https://mp.weixin.qq.com/s/z9cU60pa60-6-MUjJXZhrg)
