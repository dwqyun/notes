# ARTS第六十一周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[缺失的第一个正数](https://leetcode-cn.com/problems/first-missing-positive/)

```js
/* 
41. 缺失的第一个正数
给你一个未排序的整数数组 nums ，请你找出其中没有出现的最小的正整数。

 

进阶：你可以实现时间复杂度为 O(n) 并且只使用常数级别额外空间的解决方案吗？

 

示例 1：

输入：nums = [1,2,0]
输出：3
示例 2：

输入：nums = [3,4,-1,1]
输出：2
示例 3：

输入：nums = [7,8,9,11,12]
输出：1
 

提示：

0 <= nums.length <= 300
-231 <= nums[i] <= 231 - 1
*/

/**
 * @param {number[]} nums
 * @return {number}
 */
var firstMissingPositive = function (nums) {
  const len = nums.length;
  for (let i = 0; i < len; i++) {
    // 置换nums[nums[i] - 1] 与 nums[i] 把1到下标为 0的位置，2放到下标1位置，整理数组后再遍历一次数组，缺失的数就是第1个值不等于下标的数
    while (nums[i] > 0 && nums[i] <= len && nums[nums[i] - 1] != nums[i]) {
      [nums[nums[i] - 1], nums[i]] = [nums[i], nums[nums[i] - 1]];
    }
  }

  for (let i = 0; i < len; i++) {
    if (nums[i] != i + 1) {
      return i + 1;
    }
  }
  return len + 1;
};
```

## Review

[It’s Time To Start Using CSS Custom Properties](https://www.smashingmagazine.com/2017/04/start-using-css-custom-properties/)

## Tip

- CSS 变量一般声明于[:root](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:root)中作为全局变量，`:root`与`html`选择器相同但优先级更高

```css
:root {
  --primary-color: red;
}

p {
  color: var(--primary-color);
}
```

```js
// 判断是否支持CSS变量
const isSupported = window.CSS?.supports('--a', 0);
// document.documentElement 为文档根对象与 document.querySelector(':root') 相同
const PRIMARY_COLOR_VAR_NAME = '--primary-color';
const styles = getComputedStyle(document.documentElement);
// 获取CSS属性名称对应值
const primaryColor = String(styles.getPropertyValue(PRIMARY_COLOR_VAR_NAME)).trim();
// 移除CSS属性
document.documentElement.style.removeProperty(PRIMARY_COLOR_VAR_NAME);
// 设置CSS属性名称对应值
document.documentElement.style.setProperty(PRIMARY_COLOR_VAR_NAME, 'blue');
```

## Share

[【第2194期】SPA 路由三部曲之核心原理](https://mp.weixin.qq.com/s/DNVLuE8v0bNL3SSq7l1I_Q)
