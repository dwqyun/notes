# ARTS第三十二周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[变位词组](https://leetcode-cn.com/problems/group-anagrams-lcci/)

```js
/*
编写一种方法，对字符串数组进行排序，将所有变位词组合在一起。变位词是指字母相同，但排列不同的字符串。

注意：本题相对原题稍作修改

示例:

输入: ["eat", "tea", "tan", "ate", "nat", "bat"],
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
说明：

所有输入均为小写字母。
不考虑答案输出的顺序。
*/
/**
 * @param {string[]} strs
 * @return {string[][]}
 */
var groupAnagrams = function (strs) {
  const map = new Map();
  for (const str of strs) {
    const key = [...str].sort((a, b) => a.charCodeAt() - b.charCodeAt()).join('');
    map.has(key) ? map.set(key, [...map.get(key), str]) : map.set(key, [str]);
  }

  return [...map.values()]
};
```

## Review

[ES6 Spread and Butter in Depth](https://ponyfoo.com/articles/es6-spread-and-butter-in-depth)

## Tip

- DOM操作，最小化DOM访问次数，多次访问应该使用局部变量存储引用，注意重绘和回流，使用缓存减少布局信息访以及批量修改DOM时应该离线操作，动画也应该使用绝对定位减少布局变化及尽量使用transform、opacity只重绘的CSS属性，使用事件委托减少事件处理器数量，使用新API如querySelectorAll、firstElementChild，querySelectorAll返回的是NodeList静态集合，而getElementByClassName返回的是HTML动态集合根据文档实时更新，应该缓存HTML集合长度及拷贝为数组操作
- 使用addEventListener添加touchmove事件监听时，可判断event.touches触摸点对象，包含触摸元素及坐标，可以此实现双指缩放图片效果

## Share

[网站无障碍化简介](https://mp.weixin.qq.com/s/fsGUdGh-RedAeyMKqtd7oQ)
