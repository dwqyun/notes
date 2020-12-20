# ARTS第五十六周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)

```js
/* 
给定一个包含非负整数的 m x n 网格 grid ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

说明：每次只能向下或者向右移动一步。

 

示例 1：


输入：grid = [[1,3,1],[1,5,1],[4,2,1]]
输出：7
解释：因为路径 1→3→1→1→1 的总和最小。
示例 2：

输入：grid = [[1,2,3],[4,5,6]]
输出：12
 

提示：

m == grid.length
n == grid[i].length
1 <= m, n <= 200
0 <= grid[i][j] <= 100
*/

/**
 * @param {number[][]} grid
 * @return {number}
 */
var minPathSum = function (grid) {
  // 1.状态定义 dp为m*n矩阵 dp[i][j]代表移动到 (i,j)的最小路径和
  // 2.转移方程 取从左网格 (i-1,j)与 从上网格(i,j-1)路径和中较小的 + 当前单元格值 grid[i][j]
  // i = 0 && j = 0 => dp[i][j] = grid[i][j]
  // i = 0 && j > 0 => dp[i][j] = dp[i][j - 1]  + grid[i][j]
  // i > 0 && j = 0 => dp[i][j] = dp[i - 1][j] + grid[i][j]
  // i > 0 && j > 0 => dp[i][j] = min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j]
  // 3.初始状态 dp复用grid矩阵空间不需要修改初始值 遍历后元素不再使用 grid[i][j] = min(grid[i - 1][j], grid[i][j - 1]) + grid[i][j]
  const m = grid.length;
  const n = grid[0].length;
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (i === 0 && j === 0) {
        continue;
      }
      else if (i === 0) {
        grid[i][j] = grid[i][j - 1] + grid[i][j];
      }
      else if (j === 0) {
        grid[i][j] = grid[i - 1][j] + grid[i][j];
      }
      else {
        grid[i][j] = Math.min(grid[i - 1][j], grid[i][j - 1]) + grid[i][j]
      }
    }
  }

  return grid[m - 1][n - 1];
};
```

## Review

[Responsive Images](https://imagekit.io/responsive-images/)

## Tip

- swiper自定义transform效果，可配置`watchSlidesProgress`属性为true，监听slide滑动进度，在`touchStart、progress、setTransition`事件回调中设置样式，[`will-change`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/will-change)可以限制性动态使用在slide上

```js
var swiper = new Swiper('.swiper-container', {
  watchSlidesProgress: true,
  // other parameters
  on: {
    touchStart: function () {
      /* do something */
      this.slides.css('will-change', 'transform, opacity');
      this.slides.transition('');
    },
    progress: function () {
      /* do something */
      for (let i = 0, len = this.slides.length; i < len; i++) {
        const slide = this.slides[i];
        // slide.progress
        // slide.style.transform
      }
    },
    setTransition: function () {
      /* do something */
    },
    touchEnd: function () {
      /* do something */
      this.slides.css('will-change', 'auto');
    },
  }
});
```

## Share

[当我们谈前端性能的时候，我们谈的是什么](https://mp.weixin.qq.com/s/bjZT2u9gw7T9NbhtmykYYg)
