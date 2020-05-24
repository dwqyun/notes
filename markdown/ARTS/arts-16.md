# ARTS第十六周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/)

```js
var generateMatrix = function (n) {
  if (!n || !Number.isInteger(n)) {
    return [[]];
  }

  let left = 0;
  let right = n - 1;
  let up = 0;
  let down = n - 1;
  let res = [];
  let num = 1;

  for (let i = 0; i < n; i++) {
    res.push([]);
  }

  while (1) {
    // 上
    for (let i = left; i <= right; i++) {
      res[up][i] = num++;
    }
    if (++up > down) {
      break;
    }
    // 右
    for (let i = up; i <= down; i++) {
      res[i][right] = num++;
    }
    if (--right < left) {
      break;
    }
    // 下
    for (let i = right; i >= left; i--) {
      res[down][i] = num++;
    }
    if (--down < up) {
      break;
    }
    // 左
    for (let i = down; i >= up; i--) {
      res[i][left] = num++;
    }
    if (++left > right) {
      break;
    }
  }

  return res;
};
```

## Review

[Creating Custom Forms Using the JavaScript FormData API](https://alligator.io/js/formdata/)

## Tip

- Array().fill()中，如果fill的参数为引用类型，会导致都执行同一个引用类型。
- ...x在语义上，它用于*展开一个可迭代对象*，不是表达式不是语句不是运算符，它是逻辑的映射（它返回的是处理逻辑），而不是*值*或*引用*，通过一组特定的代码来实现展开语义。

## Share

[【第1847期】理解TypeScript 中 any 和 unknown](https://mp.weixin.qq.com/s?__biz=MjM5MTA1MjAxMQ==&mid=2651235628&idx=1&sn=425fc92e56ee3f7d455e3295d124c488&chksm=bd497ca88a3ef5be58676d9267a0bfa815397ae76093957c6dee77460000b0cacea363ac4cf5&mpshare=1&scene=23&srcid=&sharer_sharetime=1581860307333&sharer_shareid=72cab1261a060840685133c77aeb4f5f#rd)
