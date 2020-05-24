# ARTS第十九周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[多数元素](https://leetcode-cn.com/problems/majority-element/)

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function (nums) {
  return nums.sort((a, b) => a - b)[Math.ceil(nums.length / 2) - 1]
};
```

## Review

[Understanding the ECMAScript spec, part 2](https://v8.dev/blog/understanding-ecmascript-part-2)

## Tip

- 快速实现星星评分可使用flex的"flex-flow: row-reverse;" + input兄弟选择器"~"
- position:sticky粘性定位在其祖先元素的overflow属性值不是visible 时会失效，粘性定位元素超出父元素范围限制时也会失效。

## Share

[【第1877期】理解ECMAScript规范（一）](https://mp.weixin.qq.com/s/qUnJBe3r_f78c5DcUZJF3g)
