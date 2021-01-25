# ARTS第六十周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[买卖股票的最佳时机 III](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)

```js
/* 
给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 两笔 交易。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

 

示例 1:

输入：prices = [3,3,5,0,0,3,1,4]
输出：6
解释：在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
     随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。
示例 2：

输入：prices = [1,2,3,4,5]
输出：4
解释：在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。   
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。   
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
示例 3：

输入：prices = [7,6,4,3,1] 
输出：0 
解释：在这个情况下, 没有交易完成, 所以最大利润为 0。
示例 4：

输入：prices = [1]
输出：0
 

提示：

1 <= prices.length <= 105
0 <= prices[i] <= 105
*/

/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function (prices) {
  const len = prices.length;
  // 最低利润为0， 任意一天结束后有四种状态：买1 买1卖1 买2卖1 买2卖2
  let buy1 = -prices[0];
  let buy2 = -prices[0];
  let sell1 = 0;
  let sell2 = 0;

  // 状态转移 sell1->sell2 边界为0
  for (let i = 1; i < len; i++) {
    buy1 = Math.max(buy1, -prices[i]);
    sell1 = Math.max(sell1, buy1 + prices[i]);
    buy2 = Math.max(buy2, sell1 - prices[i]);
    sell2 = Math.max(sell2, buy2 + prices[i]);
  }
  return sell2;
};
```

## Review

[ES Modules in Depth](https://ui.dev/esmodules/)

## Tip

- `::-webkit-scrollbar`可以隐藏滚动条；`calc`可以嵌套计算，定义变量场景可用；`@media`支持具体宽高、宽高比查询；`@supports`可检测CSS属性是否支持，可写fallback样式

```css
::-webkit-scrollbar {
    display: none;
}

/* 媒体查询宽高: width height max-width min-width */
:root {
  --main-margin: 120px;
}
@media (min-width: 375px) and (max-width: 750px) {
  .main {
    width: calc(calc(100vw - var(--main-margin))) * 0.8;
  }
}

/* 宽高比：min-aspect-ratio  max-aspect-ratio aspect-ratio */
@media (max-aspect-ratio: 3/1) {
  div {
    border-radius: 16px;
  }
}

/* CSS属性支持检测 如检测背景是否模糊 */
div {
  background: rgba(0, 0, 0, 3);
}
@supports (backdrop-filter: blur(10)) or (-webkit-backdrop-filter: blur(10)) {
  div {
    background: rgba(0, 0, 0, 1);
    backdrop-filter: blur(10);
  }
}
```

## Share

[使用浏览器开发工具测试网站可访问性的七种方法](https://mp.weixin.qq.com/s/1EwyPjMsMKfJ4r2w7qR41g)
