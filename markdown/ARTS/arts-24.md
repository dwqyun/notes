# ARTS第二十四周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[判定字符是否唯一](https://leetcode-cn.com/problems/is-unique-lcci/)

```js
/**
 * @param {string} astr
 * @return {boolean}
 */
var isUnique = function(astr) {
  for (const char of astr) {
    if (astr.indexOf(char) !== astr.lastIndexOf(char)) {
      return false;
    }
  }
  return true;
};
```

## Review

[Tasks, microtasks, queues and schedules](https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/)

## Tip

- CSS选择器优先级数值为0的有通配选择器(*)、选择符(空格、>、+、~、||)和逻辑伪类(:not()、:is()、:where)。
- Task(macrotask)包含通常的script脚本、UI Render、setTimeout、setInterval、requestAnimationFrame，microtask有Promise、MutationObserver等，其中Vue的$nextTick就是优先使用Promise、MutationObserver下一次渲染DOM后执行回调。

## Share

[2020年前端面试复习必读文章【超百篇文章/赠复习导图】 - 掘金](https://juejin.im/post/5e8b163ff265da47ee3f54a6)
