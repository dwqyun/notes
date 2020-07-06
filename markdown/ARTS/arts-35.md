# ARTS第三十五周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[数对和](https://leetcode-cn.com/problems/pairs-with-sum-lcci/)

```js
/* 数对和
设计一个算法，找出数组中两数之和为指定值的所有整数对。一个数只能属于一个数对。

示例 1:

输入: nums = [5,6,5], target = 11
输出: [[5,6]]
示例 2:

输入: nums = [5,6,5,6], target = 11
输出: [[5,6],[5,6]]
提示：

nums.length <= 100000
*/
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[][]}
 */
var pairSums = function (nums, target) {
  if (nums.length < 2) {
    return [];
  }
  const map = new Map();
  const res = [];
  for (const num of nums) {
    // 把目标寻找值当Map 的 key
    const pair = target - num;
    const pairCounts = map.get(pair);

    if (pairCounts && pairCounts > 0) {
      res.push([num, pair]);
      // key + num === target 则key数量减一
      map.set(pair, pairCounts - 1);
    }
    else if (!map.has(num)) {
      map.set(num, 1);
    }
    else {
      map.set(num, map.get(num) + 1);
    }
  }
  return res;
};
```

## Review

[ES6 Maps in Depth](https://ponyfoo.com/articles/es6-maps-in-depth)

## Tip

- 封装一个异步的Native接口，如调用`NativeAPI.getData()`，native响应后调用`window.onDataCallback()`，可以在调用`NativeAPI.getData()`时添加自定义事件监听`window.addEventListener('customEvent', customEventCallback)`，在onDataCallback中触发自定义事件，再在自定义事件中resolve返回结果，执行A函数过程使用try-catch捕获结果与错误集

```js
// native接口回调JS方法
window.onDataCallback = data => {
  // 构造自定义事件及数据传递
  const event = new CustomEvent('customEvent', {
    detail: data
  });

  // 发布自定义事件
  window.dispatchEvent(event);
}

const eventPromise = async () => {
  try {
    const data = await new Promise((resolve) => {
      const customEventCallback = event => {
        resolve(event.detail);
      }
      window.addEventListener('customEvent', customEventCallback);
    });

    return [data, null]
  } catch (error) {
    return [undefined, error]
  }
}

const getData = async () => {
  try {
    // native接口触发
    NativeAPI.getData();
    const [data, error] = await eventPromise();
    return [data, error];
  } catch (error) {
    return [undefined, error];
  }
}
```

## Share

[【第1994期】ES11来了](https://mp.weixin.qq.com/s/GQPwA3WxAiZOKfTJIpS_Jg)
