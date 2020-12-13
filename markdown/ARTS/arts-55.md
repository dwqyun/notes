# ARTS第五十五周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[三角形最小路径和](https://leetcode-cn.com/problems/triangle/)

```js
/* 三角形最小路径和
给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。

相邻的结点 在这里指的是 下标 与 上一层结点下标 相同或者等于 上一层结点下标 + 1 的两个结点。

 

例如，给定三角形：

[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
自顶向下的最小路径和为 11（即，2 + 3 + 5 + 1 = 11）。 */
/**
 * @param {number[][]} triangle
 * @return {number}
 */
var minimumTotal = function (triangle) {
  // 相邻结点：与(i, j) 点相邻的结点为 (i + 1, j) 和 (i + 1, j + 1) 
  // dp[i][j]=min(dp[i+1][j],dp[i+1][j+1])+triangle[i][j]
  // 空间优化 dp[j]=min(dp[j],dp[j+1])+triangle[i][j]
  const len = triangle.length;
  const dp = [...triangle[len - 1]];

  for (let i = len - 2; i >= 0; i--) {
    for (let j = 0; j <= i; j++) {
      dp[j] = Math.min(dp[j], dp[j + 1]) + triangle[i][j];
    }
  }

  return dp[0];
};
```

## Review

[20 controversial programming opinions](https://programmers.blogoverflow.com/2012/08/20-controversial-programming-opinions/)

## Tip

- 绝对定位fixed元素相对于body视口的位置定位，会创建新的层叠上下文，但当其祖先元素的属性 transform,、perspective 或 filter 非 none 时，则相对于该祖先定位，在使用fixed绝对定位需要注意相对于哪一视口定位；fixed用于body场景可以限定弹框内容滚动时不触发body滚动。
- overflow-anchor设置浏览器滚动瞄定，支持滚动锚定行为的浏览器默认会调整滚动位置减少内容偏移，如img标签加载图片内容变高但滚动位置不变，需要关闭此行为时才改值`overflow-anchor: none;`，如果页面顶部是图片可以使用padding相对宽度设置div高度预加载占位

## Share

[纯CSS实现微信列表左滑显示按钮的交互效果](https://www.zhangxinxu.com/wordpress/2020/12/css-touch-scroll-show-button/)
