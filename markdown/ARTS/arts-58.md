# ARTS第五十八周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

```js
/* 

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

示例 1：

输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1
示例 2:

输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
提示：

2 <= n <= 58
*/

/**
 * @param {number} n
 * @return {number}
 */
var cuttingRope = function (n) {
  if (n < 4) {
    return n - 1;
  }

  // 大于3的数可拆分为1、2、3的和，对3余数为0、1、2，数学上尽可能分为3的段乘积最大
  // dp[0]，dp[1]，dp[2] 表示所有大于 3 的值
  const dp = [0, 1, 1];

  for (let i = 4; i < n + 1; i++) {
    dp[i % 3] = Math.max(
      Math.max(dp[(i - 1) % 3], i - 1),
      2 * Math.max(dp[(i - 2) % 3], i - 2),
      3 * Math.max(dp[(i - 3) % 3], i - 3)
    )
  }

  return dp[n % 3]
};
```

## Review

[Thinking Outside the Box with CSS Grid](https://frontend.horse/articles/thinking-outside-the-box-with-css-grid/)

## Tip

- HTML超链接`a`标签元素可以添加`download`属性实现如canvas截图后转为blob或base64数据下载，`href`为URL片段或URL可以使用浏览器支持的协议，如移动H5中可用协议`mailto:`拉起邮箱，`tel:`拉起电话，`intent:`[Chrome唤醒APP](https://developer.chrome.com/docs/multidevice/android/intents/)，QQ、UC等用`scheme:`唤醒APP

```html
<!-- https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a -->
<ul>
  <li><a href="intent://scan/#Intent;scheme=zxing;package=com.google.zxing.client.android;end"> zxing </a></li>
  <li><a href="zxing://scan/"> zxinge </a></li>
  <li><a href="mailto:m.bluth@example.com">Email</a></li>
  <li><a href="tel:+123456789">Phone</a></li>
</ul>
<!-- https://developer.mozilla.org/zh-CN/docs/Web/Guide/HTML/Email_links -->
<!-- 发送邮件可指定主题subject、抄送人cc、密送人bcc、邮件内容body，每个字段值需要进行编码 -->
<a href="mailto:nowhere@mozilla.org?subject=Newsletter%20subscription%20request&body=Please%20subscribe%20me%20to%20your%20newsletter!%0A%0AFull%20name%3A%0A%0AWhere%20did%20you%20hear%20about%20us%3F">
Subscribe to our newsletter
</a>
```

## Share

[【第2172期】自适应布局最佳实践](https://mp.weixin.qq.com/s/8GvZetosiFJmZ1n3ZLfxNA)
