# ARTS第四十七周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

```js
/* 礼物的最大价值
在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？



示例 1:

输入:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 12
解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物


提示：

0 < grid.length <= 200
0 < grid[0].length <= 200 */
/**
 * @param {number[][]} grid
 * @return {number}
 */
var maxValue = function (grid) {
  // m*n 行列
  const m = grid.length;
  const n = grid[0].length;
  /* 状态转移表法 增一行一列便于计算grid[0][0]到grid[i - 1][j - 1]的最大值
  [
    [0,0,0,0],
    [0,1,4,5],
    [0,2,max(1+2, 1+4),max..,max..],
    [0,6,max..,max..]
  ]
  */
  let states = new Array(m + 1).fill(new Array(n + 1).fill(0));

  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      // 向下(i-1, j)和向右(i, j-1) 两个位置对应的状态计算(i, j)  转移方程如下
      states[i][j] = grid[i - 1][j - 1] + Math.max(states[i][j - 1], states[i - 1][j]);
    }

  }

  return states[m][n];
};
```

## Review

[10 lesser-known Web APIs you may want to use](https://blog.greenroots.info/10-lesser-known-web-apis-you-may-want-to-use-ckejv75cr012y70s158n85yhn)

## Tip

- 浏览器的默认行为contextmenu、mousedown、keydown、submit，通过JavaScript处理所有默认行为都是可以被阻止的，可以使用 `event.preventDefault()` 或 `return false`(只适用于通过 on* 特性（attribute） 分配的处理程序)，addEventListener 的 `passive: true` 选项告诉浏览器该行为不会被阻止，对于某些移动端的事件（像 touchstart 和 touchmove）很有用，用以告诉浏览器在滚动之前不应等待所有处理程序完成，可用于滚动事件性能优化

如果默认行为被阻止，event.defaultPrevented 的值会变成 true，否则为 false

```html
<a href="https://w3.org" onclick="return handler1()">w3.org</a>
<a href="https://w3.org" onclick="handler2(event)">w3.org</a>
<script>
  function handler1() {
    return false;
  }
  function handler2(event) {
    event.preventDefault();
  }
</script>
```

## Share

[理解ECMAScript规范（二）](https://mp.weixin.qq.com/s/JRHP-YyW_z7oZZXUG17p9Q)
