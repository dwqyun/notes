# ARTS第十四周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[存在重复元素](https://leetcode-cn.com/problems/contains-duplicate/)

```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function(nums) {
  while (nums.length) {
    let temp = nums.splice(0, 1);
    if (nums.includes(temp[0])) {
      return true;
    }
  }
  return false;
};
```

## Review

[3 Ways To Replace All String Occurrences in JavaScript](https://dmitripavlutin.com/replace-all-string-occurrences-javascript/)

## Tip

- for 循环中添加块语句时每次迭代中都会都会创建块级作用域副本，层次越多、引用越复杂，这类情况下并不比使用函数递归节省开销，需要相应减少作用域。
- 模板字面量是一种特殊的可执行结构，执行结果是一个字符串。

## Share

[【第1738期】100 行代码实现 Promises/A+ 规范](https://mp.weixin.qq.com/s/Yrwe2x6HukfqJZM6HkmRcw)
