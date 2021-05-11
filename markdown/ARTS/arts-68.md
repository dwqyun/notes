# ARTS第六十八周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[数组中重复的数据](https://leetcode-cn.com/problems/find-all-duplicates-in-an-array/)

```js
/* 
给定一个整数数组 a，其中1 ≤ a[i] ≤ n （n为数组长度）, 其中有些元素出现两次而其他元素出现一次。

找到所有出现两次的元素。

你可以不用到任何额外空间并在O(n)时间复杂度内解决这个问题吗？

示例：

输入:
[4,3,2,7,8,2,3,1]

输出:
[2,3]
*/

/**
 * @param {number[]} nums
 * @return {number[]}
 */
var findDuplicates = function (nums) {
  const res = [];
  if (nums.length === 0) {
    return res;
  }

  // 元素值在1~n 通过绝对值和索引映射 可原地修改元素值为负值标记已访问
  for (const num of nums) {
    const index = Math.abs(num) - 1;
    if (nums[index] < 0) {
      res.push(Math.abs(num));
    }
    nums[index] = -nums[index];
  }
  return res;
};
```

## Review

[CSS Tips](https://markodenic.com/css-tips/)

## Tip

- CSS 小技巧
  - [cursor](https://developer.mozilla.org/zh-CN/docs/Web/CSS/cursor) CSS 属性设置鼠标指针悬停在元素上时光标样式，可使用`url()`显示自定义图片
  - [::selection](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::selection) CSS 伪元素应用于文档中被用户高亮的部分，可修改高亮色
  - [caret-color](https://markodenic.com/css-tips/) 来定义插入光标的颜色

```css
/* 使用URL，并可提供备用值 */
.image-cursor {
  cursor: url(one.svg), auto;
}

.highlighting::selection {
  background-color: #007dff;
  color: #fff;
}

input {
  caret-color: red;
}
```

## Share

[软件工程的最大难题](https://mp.weixin.qq.com/s/WO5z13Sz-AGuF3IEzIC3fA)