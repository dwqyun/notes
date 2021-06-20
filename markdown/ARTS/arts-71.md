# ARTS第七十一周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[颜色分类](https://leetcode-cn.com/problems/sort-colors/)

```js
/* 
给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

示例 1：
输入：nums = [2,0,2,1,1,0]
输出：[0,0,1,1,2,2]

示例 2：
输入：nums = [2,0,1]
输出：[0,1,2]

提示：

n == nums.length
1 <= n <= 300
nums[i] 为 0、1 或 2
*/

/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
const sortColors = (nums) => {
  const len = nums.length;
  // 交互位置指针
  let ptr = 0;

  // 第一次遍历将数组中所有的0交换到头部,第二次遍历将数组中所有的1交换到头部,所有的2都出现在数组的尾部
  for (let i = 0; i < len; ++i) {
    if (nums[i] === 0) {
      // 将值为0的项交换到左边
      [nums[i], nums[ptr]] = [nums[ptr], nums[i]];
      ++ptr;
    }
  }
  // 从0之后的位置开始遍历
  for (let i = ptr; i < len; ++i) {
    if (nums[i] === 1) {
      // 将值为1的项交换到左边
      [nums[i], nums[ptr]] = [nums[ptr], nums[i]];
      ++ptr;
    }
  }

  return nums;
};
```

## Review

[HTML Tips](https://markodenic.com/html-tips/)

## Tip

- [Navigator.sendBeacon()](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/sendBeacon) 使用
  - `window.navigator.sendBeacon(url, data)` 方法可用于通过HTTP将少量数据异步传输到Web服务器，`url`为发送data的服务器地址，`data`可以是ArrayBufferView 、 Blob、DOMString 或 FormData 类型
  - 实际应用场景可以是数据埋点上报，即时页面被卸载浏览器也可以将请求发出

```js
/* 来自MDN： 使用 sendBeacon() 方法会使用户代理在有机会时异步地向服务器发送数据，同时不会延迟页面的卸载或影响下一导航的载入性能 */
window.addEventListener('unload', logData, false);

function logData() {
    navigator.sendBeacon("/log", analyticsData);
}
```

## Share

[JavaScript 事件循环：从起源到浏览器再到 Node.js](https://mp.weixin.qq.com/s/E0vu7kJLcgDdJRVrAeyEIA)
