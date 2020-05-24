# ARTS第一周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[两数之和](https://leetcode-cn.com/explore/interview/card/tencent/221/array-and-strings/894/)

- 使用Map存储数字之和等于目标数的值和下标
- 只使用一次for循环

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
let twoSum = (nums, target) => {
    if (!Array.isArray(nums) || typeof target !== 'number') {
        return [];
    }
    const temp = new Map();
    const i = nums.findIndex((val, index) => temp.has(target - val) || temp.set(val, index) && 0);
    return [temp.get(target - nums[i]), i];
};
```

## Review

[7 Useful JavaScript Tricks](https://davidwalsh.name/javascript-tricks)

1. 使用Set集合获取不重复的数组
2. 使用Array的map和filter方法过滤真假值
3. 使用Object.create(null)创建空字典对象
4. 使用...扩展运算符合并对象
5. 使用函数默认参数校验函数入参
6. 使用解构时可起别名避免命名冲突
7. 使用URLSearchParams获取URL参数

## Tip

- 监听横向纵向滚动到底触发自动加载可先寻找滚动元素scrollingElement，判断滚动盒子的可视宽高加滚动距离是否大于等于内容区域真实宽高：clientHeight + scrollTop >= scrollHeight | clientWidth + scrollLeft >= scrollWidth
- lottie-web使用JSON时，webpack可能会将图片压缩为base64故可修改JSON中图片路径asserts传入为base64，且添加DOM_Load可根据数据状态切换帧显示

## Share

[【第1689期】职业思考：技术人需要突破的 10 个困局](https://mp.weixin.qq.com/s/4bniPjbHzqMDFDkxb6_i9Q)
