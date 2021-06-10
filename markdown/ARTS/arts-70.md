# ARTS第七十周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[删除有序数组中的重复项 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array-ii/)

```js
/* 
给你一个有序数组 nums ，请你 原地 删除重复出现的元素，使每个元素 最多出现两次 ，返回删除后数组的新长度。

不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

 

说明：

为什么返回数值是整数，但输出的答案是数组呢？

请注意，输入数组是以「引用」方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
 

示例 1：

输入：nums = [1,1,1,2,2,3]
输出：5, nums = [1,1,2,2,3]
解释：函数应返回新长度 length = 5, 并且原数组的前五个元素被修改为 1, 1, 2, 2, 3 。 不需要考虑数组中超出新长度后面的元素。
示例 2：

输入：nums = [0,0,1,1,1,1,2,3,3]
输出：7, nums = [0,0,1,1,2,3,3]
解释：函数应返回新长度 length = 7, 并且原数组的前五个元素被修改为 0, 0, 1, 1, 2, 3, 3 。 不需要考虑数组中超出新长度后面的元素。
 

提示：

1 <= nums.length <= 3 * 104
-104 <= nums[i] <= 104
nums 已按升序排列
*/

/**
 * @param {number[]} nums
 * @return {number}
 */
 var removeDuplicates = function(nums) {
  const n = nums.length;
  // 有序数组可直接保留前两位
  if (n <= 2) {
      return n;
  }
  // 定义慢指针标识处理好的数组长 快指针标识检查过的数组长
  let slow = 2, fast = 2;
  while (fast < n) {
      // 元素可出现两次 检查上一次保留的数（当前前两位的数）是否和当前数相同 不相同则保留
      if (nums[slow - 2] != nums[fast]) {
          nums[slow] = nums[fast];
          ++slow;
      }
      ++fast;
  }
  return slow;
};
```

## Review

[CSS Functions](https://web.dev/learn/css/functions/)
  - Functional selectors： :is()、:not()
  - Custom properties:var()
  - Functions that return a value : attr(), url()
  - Color functions: rgb(),  rgba(), hsl(), hsla()
  - Mathematical expressions: calc(), min(), max(), clamp()
  - Shapes( clip-path, offset-path and shape-outside): circle(), ellipse(), inset(), path()
  - Transforms, perspective: rotate(), scale(), translate(), skew()
  - Animation functions, gradients and filters


## Tip

- CSS控制用户行为
  - `user-select`控制用户能否选中文本，值为`none`不可选中元素及其子元素文本
  - `user-modify`控制是否允许输入框输入内容、是否只允许输入纯文本，值为`read-write-plaintext-only`时不可输入富文本
  - `user-drag`控制是否允许用户拖拽页面，样式`-webkit-user-drag: none;`和标签属性`draggable="true"`相关相同


```css
.unselectable {
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.readwrite {
  -moz-user-modify: read-write;
  -webkit-user-modify: read-write;
}
.undraggable {
  -webkit-user-drag: none;
}
```

## Share

[使用 axios 拦截器解决「 前端并发冲突 」 问题](https://mp.weixin.qq.com/s/ehNvVfey1zqG6L4WY0GHRQ)
