# ARTS第三十周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[旋转矩阵](https://leetcode-cn.com/problems/rotate-matrix-lcci/)

```js
/*
给你一幅由 N × N 矩阵表示的图像，其中每个像素的大小为 4 字节。请你设计一种算法，将图像旋转 90 度。

示例:

给定 matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
]

原地旋转输入矩阵，使其变为:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var rotate = function (matrix) {
  const len = matrix.length;
  if (len === 0) {
    return;
  }
  // 以十字架分割 计算左上角区域行列下标
  const row = (len >> 1) - 1;
  const col = (len - 1) >> 1;

  for (let i = row; i >= 0; --i) {
    for (let j = col; j >= 0; --j) {
      // 左上角第i行第j列元素 旋转后位于右上角第j行倒数第i列 解构交换即交换示例值4<->8
      [matrix[i][j], matrix[j][len - i - 1]] = [matrix[j][len - i - 1], matrix[i][j]];
      // 左上角第i行第j列元素 交换右下角倒数第j行倒数第i列 即交换示例值8<->6
      [matrix[i][j], matrix[len - i - 1][len - j - 1]] = [matrix[len - i - 1][len - j - 1], matrix[i][j]];
      // 左上角第i行第j列元素 交换左下角倒数第j行第i列 即交换示例值6<->3
      [matrix[i][j], matrix[len - j - 1][i]] = [matrix[len - j - 1][i], matrix[i][j]];
    }
  }
};
```

## Review

[Extending the Limits of CSS](https://www.welcometothejungle.com/en/articles/btc-css-limits)

## Tip

- CSS columns可实现不改变display值同时达到两端布局效果，如在ul>li下使用Flex布局和Grid布局的space-between值实现两端对齐，会移除li标签的项符号，此场景使用`columns: 3 30px;`即可实现固定列数间隔和两端对齐
- 对象是对数据的封装，解构是从封装的对象中抽取数据，对象本质是关联数组(不可索引的数据结构，名值对创建的数组)，数组是索引数组(可索引的，被存取的数据关联的名字就是索引)，如`a = 100, b = 200; [a, b] = {a, b}`中，若右操作数成为一个`可迭代对象`，赋值表达式就可将它赋给左侧的赋值模板，可使用`Symbol`和`Generator`构造对象的遍历器方法`Object.prototype[Symbol.iterator] = function*() { yield* Object.values(this); };`，即将对象成员的列举变为对象成员值的列举时关联数组可做索引数组使用，实际代码使用中可写为`[a, b] = Object.values({a, b})`，反之将数组赋值给对象赋值模板，需要确认索引与名字的对应关系`({0: x, 1: y} = [a, b])`，赋值过程受原型影响，可使用`展开运算符`将数组展开到一个对象`obj = {...[a,b]}`实现浅拷贝

## Share

[提高代码使用率](https://mp.weixin.qq.com/s/YsMTJa8iYGAW6mRyV0JOZQ)
