# ARTS第三十三周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[2出现的次数](https://leetcode-cn.com/problems/number-of-2s-in-range-lcci/submissions/)

```js
/* 2出现的次数
编写一个方法，计算从 0 到 n (含 n) 中数字 2 出现的次数。

示例:

输入: 25
输出: 9
解释: (2, 12, 20, 21, 22, 23, 24, 25)(注意 22 应该算作两次)
提示：

n <= 10^9 */
/**
 * @param {number} n
 * @return {number}
 */
var numberOf2sInRange = function (n) {
  // 计数
  let count = 0;
  // 当前位
  let cur = 0;
  // 当前位后数值
  let last = 0;

  while (n) {
    // 取个位
    const unit = n % 10;
    // 取非个位
    const ununit = Math.floor(n / 10);
    // 规律是10的次幂次 再根据模添加额外次数
    count += ununit * (10 ** cur);
    if (unit === 2) {
      count += last + 1;
    }
    if (unit > 2) {
      count += 10 ** cur;
    }
    last += unit * (10 ** cur);
    cur += 1;
    n = ununit;
  }

  return count;
};
```

## Review

[Property order is predictable in JavaScript objects since ES2015](https://www.stefanjudis.com/today-i-learned/property-order-is-predictable-in-javascript-objects-since-es2015/)

## Tip

- ES2015前JavaScript对象属性顺序不可预测，如for-in、Object.keys、JSON.stringify，从ES2015开始ownPropertyKeys对象内置方法实现了属性顺序的定义，例如Reflect.ownKeys、Object.getOwnPropertyNames、Object.defineProperties内部使用ownPropertyKeys方法，按整数索引、字符串、Symbol排序
- 当元素几何和位置属性变化时，浏览器通过队列优化批量执行重排过程，但一些无意的DOM操作会强制刷新队列立即触发重排，如最新布局信息API方法或属性`(offset|scroll|client)Top、(offset|scroll|client)Left、(offset|scroll|client)Width、(offset|scroll|client)Height、getComputedStyle()|currentStyle`，应该通过缓存、离线方式批量操作DOM，例如使用cssText属性增量一次性更新样式信息

## Share

[ECMAScript 规范阅读导引 Part 1](https://mp.weixin.qq.com/s/t1y4tlN83a2eCjtuMDDelA)
