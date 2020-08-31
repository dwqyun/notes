# ARTS第四十二周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[栈的压入、弹出序列](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof)

```js
/* 输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。



示例 1：

输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
输出：true
解释：我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
示例 2：

输入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
输出：false
解释：1 不能在 2 之前弹出。


提示：

0 <= pushed.length == popped.length <= 1000
0 <= pushed[i], popped[i] < 1000
pushed 是 popped 的排列。 */

/**
 * @param {number[]} pushed
 * @param {number[]} popped
 * @return {boolean}
 */
var validateStackSequences = function (pushed, popped) {
  const stack = [];
  let index = 0;
  for (let i = 0, len = pushed.length; i < len; i++) {
    stack.push(pushed[i]);
    // 压栈副本尾元素与pop弹出队列元素对比
    while (stack.length !== 0 && stack[stack.length - 1] === popped[index]) {
      stack.pop();
      index++;
    }
  }
  return !stack.length;
};
```

## Review

[Make All Images on Your Website Responsive in 3 Easy Steps](https://ponyfoo.com/articles/make-all-images-on-your-website-responsive-in-3-easy-steps)

## Tip

- `background-image: url(xxx)`支持动画和过渡效果`transition: background-image 1s;`
- async/await语法结合Promise可以将回调函数写为同步化代码，如setTimeout、event listener、网络I/O订阅事件等callback

```js
  // 定时器回调
  function sleep(time) {
    return new Promise((resolve, reject) => {
      setTimeout(resolve, time);
    })
  }

  await sleep(1000);

  // 事件回调
  function awaitEvent(element, eventName) {
    return new Promise((resolve, reject) => {
      element.addEventListener(eventName, resolve);
    })
  }

  // 构造自定义事件及数据传递
  const customEvent = new CustomEvent('customEventName', {
    detail: 'data'
  });

  function awaitCustomEvent() {
    return new Promise((resolve, reject) => {
      window.addEventListener('customEventName', event => {
        resolve(event.detail);
      });
    })
  }
  await awaitCustomEvent();

  // 发布自定义事件
  window.dispatchEvent(customEvent);
```

## Share

[网页布局都有哪种？一般都用什么布局？](https://mp.weixin.qq.com/s/WX4tZkP_EXjcxuRcNBwfmQ)
