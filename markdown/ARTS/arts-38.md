# ARTS第三十八周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[完全平方数](https://leetcode-cn.com/problems/perfect-squares/submissions/)

```js
/*
给定正整数 n，找到若干个完全平方数（比如 1, 4, 9, 16, ...）使得它们的和等于 n。你需要让组成和的完全平方数的个数最少。

示例 1:

输入: n = 12
输出: 3
解释: 12 = 4 + 4 + 4.
示例 2:

输入: n = 13
输出: 2
解释: 13 = 4 + 9. */

/**
 * @param {number} n
 * @return {number}
 */
var numSquares = function (n) {
  // 缓存每个数的平方集合
  const dp = Array(n + 1).fill(0);
  for (let i = 1; i <= n; i++) {
    dp[i] = i;
    for (let j = 1; i - j * j >= 0; j++) {
      // ƒ(n - k * k) + 1 = ƒ(n); d = n - k * k 总取最大平方数
      dp[i] = Math.min(dp[i], dp[i - j * j] + 1);
    }
  }
  return dp[n];
};
```

## Review

[My website now loads in less than 2 sec! Here's how I did it!](https://dev.to/cmcodes/my-website-now-loads-in-less-than-2-sec-here-s-how-i-did-it-hoj)

## Tip

- 目前主流浏览器都提供了 `Web Animations API` 支持，可以通过API编程提供 `CSS Animations`和 `CSS Transitions` 的能力，可以使用事件回调控制动画，无逻辑动画可以使用Lottie库实现

## Share

[【第2015期】Web Worker 文献综述](https://mp.weixin.qq.com/s/MyRRIbn-UoruVD1dpvD-QQ)
