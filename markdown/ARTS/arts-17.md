# ARTS第十七周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

```js
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function (nums1, m, nums2, n) {
  nums1.splice(m, m + n, ...nums2);
  nums1 = nums1.sort((a, b) => a - b);
};
```

## Review

[fixing-memory-leaks-in-web-applications](https://nolanlawson.com/2020/02/19/fixing-memory-leaks-in-web-applications/)

## Tip

- img元素是可替换元素，当图片加载失败时，伪元素才可以显示（有兼容问题），此时可以使用伪元素为裂图设置样式，content结合attr()函数显示图片描述。
- 相对地址转换为绝对地址可以使用new URL(url, [base])方法，兼容可以使用a元素href拼接赋值返回。

## Share

[【第1864期】手撕Git，告别盲目记忆](https://mp.weixin.qq.com/s?__biz=MjM5MTA1MjAxMQ==&mid=2651235750&idx=1&sn=bdc3d6938b34638c3868d3c69e763f8b&chksm=bd497c228a3ef53478d4c6e9cf3f266f684dc76525917674d0bfa91d50e757837e7545480492&mpshare=1&scene=23)
