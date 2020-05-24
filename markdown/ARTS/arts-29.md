# ARTS第二十九周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[字母与数字](https://leetcode-cn.com/problems/find-longest-subarray-lcci/submissions/)

```js
/*
给定一个放有字符和数字的数组，找到最长的子数组，且包含的字符和数字的个数相同。

返回该子数组，若存在多个最长子数组，返回左端点最小的。若不存在这样的数组，返回一个空数组。

示例 1:

输入: ["A","1","B","C","D","2","3","4","E","5","F","G","6","7","H","I","J","K","L","M"]

输出: ["A","1","B","C","D","2","3","4","E","5","F","G","6","7"]
 */
/**
 * @param {string[]} array
 * @return {string[]}
 */
var findLongestSubarray = function (array) {
 // 字母视为-1 数字视为1 使用map存储数组索引对应的字母数字个数
 const map = new Map([[0, -1]]);
 let total = 0;
 let begin = 0;
 let end = 0;
 let find = false;
 for (let i = 0; i < array.length; i++) {
 if (/[0-9]/.test(array[i])) {
 total += 1;
    }
 else {
 total -= 1;
    }

 if (!map.has(total)) {
 // 记录每个值第一次遇到的index
 map.set(total, i);
    }
 // 已有相同total值时对应前后索引
 else if (i - map.get(total) > end - begin) {
 find = true;
 begin = map.get(total);
 end = i;
    }
  }
 return find ? array.slice(begin + 1, end + 1) : []
};
```

## Review

[Monitor your web page's total memory usage with measureMemory()](https://web.dev/monitor-total-page-memory-usage/)

## Tip

- Vue中provide / inject 用于祖先向后代组件传递数据和方法，是大范围性的props，如果传入可响应式的对象子组件中 inject 的对象也可以动态变化，inject 可以用于props和data属性值的初始化，provide / inject声明顺序写在props和data前便于阅读。
- 使用正则模拟URLSearchParams获取和设置URL参数，获取参数key的值使用"new RegExp(`[\\?|&]key=([^&#]*)`).exec(location.search);"匹配后去结果第一个"decodeURIComponent(results[1].replace(/\+/g,''));"，更新key参数值为value为“location.search.replace(new RegExp(`([\?&])key=[^&]*`), "$1key=value");”，移除key=value&为"location.search.replace(new RegExp(`([\?&])safe=[^&;]+[&;]?`), "$1");"

## Share

[Vue源码详解之nextTick](https://github.com/Ma63d/vue-analysis/issues/6)
