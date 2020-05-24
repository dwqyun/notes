# ARTS第八周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
  let len = 1;
  for (let i = 1; i < nums.length; i++) {
    if (nums[i] != nums[i - 1]) {
      nums[len++] = nums[i];
    }
  }
  return len
};
```

## Review

[Are There Random Numbers in CSS? | CSS-Tricks](https://css-tricks.com/are-there-random-numbers-in-css/)

## Tip

- 富文本编辑器quill简单易扩展，可自定义toolbar图标及其事件处理,如添加undo、redo功能；可使用quill.root.innerHTML 获取HTML内容，使用getContent方法可以获取到Delta，可从Delta中拼接图文视频混排的摘要。
- div的placeholder显示可以使用伪元素content结合attr函数获取dataset中绑定的占位文本

## Share

[【第1764期】小程序工程化探索：大规模场景下的问题和解决方案](https://mp.weixin.qq.com/s/O-J2mbxIWKG5dUXP0IBAcw)
