# ARTS第四十六周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[数组中数字出现的次数 II](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

```js
/* 数组中数字出现的次数 II
在一个数组 nums 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。



示例 1：

输入：nums = [3,4,3,3]
输出：4
示例 2：

输入：nums = [9,1,7,9,7,9,7]
输出：1


限制：

1 <= nums.length <= 10000
1 <= nums[i] < 2^31
  */
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function (nums) {
  let res = 0;
  for (let i = 0; i < 32; i++) {
    // 计数
    let count = 0;
    // 左移 *2
    let bit = 1 << i;
    for (let j = 0; j < nums.length; j++) {
      if (nums[j] & bit) {
        count++;
      }

    }
    // 对出现次数取 3 余数
    if (count % 3 !== 0) {
      res = res | bit;
    }
  }
  return res;
};
```

## Review

[10 useful HTML5 features, you may not be using](https://dev.to/atapas/10-useful-html5-features-you-may-not-be-using-2bk0)

## Tip

- Mutation observer(DOM 变动观察器)，是一个内建对象，用于观察 DOM 元素，在其发生更改时触发回调，可用于跟踪代码其他部分引入的DOM更改如动态代码的高亮显示、删除第三方脚本生成的DOM；vue2之前有使用过MutationObserver作为Promise的降级处理方案，属于microtask，下一次渲染DOM后执行回调

```html
<div contentEditable id="ele">Click and <b>edit</b>, please</div>

<script>
// 带有回调函数的观察对象
let observer = new MutationObserver(mutationRecords => {
  for(let mutation of mutations) {
    // 检查新节点，有什么需要高亮显示的吗？

    for(let node of mutation.addedNodes) {
      // 跟踪元素节点
      if (!(node instanceof HTMLElement)) continue;
      // ...
    }
  }
  console.log(mutationRecords); // MutationRecord 对象列表传入第一个参数
});

// 附加到一个 DOM 节点 config为观察器的配置 观察除了特性之外的所有变动
observer.observe(document.getElementById('ele'), {
  attributes: false,
  childList: true, // 观察直接子节点
  subtree: true, // 及其更低的后代节点
  characterDataOldValue: true // 将旧的数据传递给回调
});
// 可停止观察
observer.disconnect();
// 处理未处理的变动
let mutationRecords = observer.takeRecords();
</script>
```

## Share

[如何提升职业工作效率](https://mp.weixin.qq.com/s/zH9kFjJQ5zE9mKGEiwEYAA)
