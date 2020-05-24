# ARTS第七周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
  if (s === '') {
    return true;
  }
  if (s == null || s.length % 2 !== 0 || !/[\(\)\{\}\[\]]/.test(s)) {
    return false;
  }
  const map = new Map([
    ['(', ')'],
    ['{', '}'],
    ['[', ']']
  ]);
  const stack = ['?']

  for (let char of s) {
    if (map.get(char)) {
      stack.push(char);
    }
    else if (map.get(stack.pop()) !== char) return false;
  }
  return stack.length === 1;
};
```

## Review

[Faster Web Applications with Vue 3 - Vue.js Tutorials](https://vueschool.io/articles/vuejs-tutorials/faster-web-applications-with-vue-3/)

## Tip

- 只聚焦不滚动button.focus({ preventScroll: true });
- document.readyState(loading-interactive-complete)的使用场景，DOMContentLoaded事件绑定在页面的准备状态loading变为interactive时执行，interactive变为complete执行load事件。
- textarea自动增高，先初始设置height样式属性值为auto、scrollTop为0，内容变化时设置height为内容高度scrollHeight。

## Share

[【第1756期】「Shape Up」 适合中小团队的一种工作方式](https://mp.weixin.qq.com/s?__biz=MjM5MTA1MjAxMQ==&mid=2651234365&idx=1&sn=565d84f0dc8b04af6d039e08def51090&chksm=bd4979b98a3ef0af121ab982b53eacfa511abc83612e74a450a1110d1c55d792bdcb1556c5b8&mpshare=1&scene=23&srcid=&sharer_sharetime=1572169163252&sharer_shareid=72cab1261a060840685133c77aeb4f5f#rd)
