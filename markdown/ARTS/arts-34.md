# ARTS第三十四周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[稀疏数组搜索](https://leetcode-cn.com/problems/sparse-array-search-lcci/)

```js
/* 稀疏数组搜索
有个排好序的字符串数组，其中散布着一些空字符串，编写一种方法，找出给定字符串的位置。

示例1:

 输入: words = ["at", "", "", "", "ball", "", "", "car", "", "","dad", "", ""], s = "ta"
 输出：-1
 说明: 不存在返回-1。
*/
/**
 * @param {string[]} words
 * @param {string} s
 * @return {number}
 */
var findString = function (words, s) {
  const map = new Map();
  for (let index = 0; index < words.length; index++) {
    map.set(words[index], index);
  }
  return map.has(s) ? map.get(s) : -1;
};
```

## Review

[Quick & Dirty Theme Switcher](https://uglyduck.ca/quick-dirty-theme-switcher/)

## Tip

- 改善循环性能的最佳方式是减少迭代的运算量和减少循环迭代次数，如可使用函数自身缓存对象，减少重复计算；避免使用for-in除非确定要遍历属性数量未知对象，查找集合比if-else和switch更快

- CSS text-emphasis属性可用于文字强调装饰，text-emphasis-color控制颜色，text-emphasis-style控制装饰符形状效果，text-emphasis-position控制装饰符位置

## Share

[【第1979期】深入理解 Vue3 Reactivity API](https://mp.weixin.qq.com/s/mnsI8MxBmhomttV0UXWSyg)
