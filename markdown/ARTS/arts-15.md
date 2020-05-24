# ARTS第十五周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[螺旋矩阵](https://leetcode-cn.com/problems/spiral-matrix/)

```js
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function (matrix) {
  if (!Array.isArray(matrix) || !matrix.length || !matrix[0].length) {
    return [];
  }

  const m = matrix.length;
  const n = matrix[0].length;
  let left = 0;
  let right = n - 1;
  let up = 0;
  let down = m - 1;
  let res = [];

  while (1) {
    // 上
    for (let i = left; i <= right; i++) {
      res.push(matrix[up][i]);
    }
    if (++up > down) {
      break;
    }
    // 右
    for (let i = up; i <= down; i++) {
      res.push(matrix[i][right]);
    }
    if (--right < left) {
      break;
    }
    // 下
    for (let i = right; i >= left; i--) {
      res.push(matrix[down][i]);
    }
    if (--down < up) {
      break;
    }
    // 左
    for (let i = down; i >= up; i--) {
      res.push(matrix[i][left]);
    }
    if (++left > right) {
      break;
    }
  }
  return res;
};
```

## Review

[NaN in JavaScript](https://dmitripavlutin.com/nan-in-javascript/)

## Tip

- overscroll-behavior:contain让滚动嵌套时父滚动不触发
- 可中断语句`break;`包括全部的循环语句，以及 switch 语句，中断**任意的标签化语句**`break labelName;`中断当前语句将执行逻辑交到下一语句;语句执行的返回结果是该命令得以完成的状态结果，函数是求值结果，结果包括normal、break、continue、return、throw。

## Share

[【第1828期】种草 ES2020 新特性](https://mp.weixin.qq.com/s?__biz=MjM5MTA1MjAxMQ==&mid=2651235405&idx=1&sn=6da042f4b37c4159b35f3175d7518a6d&chksm=bd497dc98a3ef4df1ff480d1a6a602c160cf577b965c2294bb05e512135e158d7e5930bd1576&mpshare=1&scene=23&srcid=&sharer_sharetime=1578806961717&sharer_shareid=72cab1261a060840685133c77aeb4f5f#rd)
