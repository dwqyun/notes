# ARTS第九周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)

```js
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function (height) {
  if (!Array.isArray(height)) {
    return 0;
  }
  const len = height.length;
  let max = 0;
  let l = 0;
  let r = len - 1;
  while (l < r) {
    max = Math.max(max, Math.min(height[l], height[r]) * (r - l));
    if (height[l] < height[r]) {
      l++;
    } else {
      r--;
    }
  }
  return max;
};
```

## Review

[HTTP Cats](https://http.cat/)

## Tip

- 动态使用innerHTML插入DOM判断，需要注意XSS攻击，可使用js-xss的白名单功能控制HTML标签及属性显；普通文本使用textContent赋值即可。
- JS检测浏览器是否支持某CSS属性，可以使用CSS.supports，如要检测IE可使用document.body.style.hasOwnProperty检测属性，检测属性值可以使用setAttribute设置CSS声明后判断其返回值。

## Share

[【第1777期】阿里舒文：从应届生到双11前端PM](https://mp.weixin.qq.com/s?__biz=MjM5MTA1MjAxMQ==&mid=2651234665&idx=1&sn=d617a1ca86f2121f92e910666e40bcd1&chksm=bd4978ed8a3ef1fb7f1e20c816311174fd5f8aec7b7d165018b2bc0e4dd1f88a4a2bd197578e&mpshare=1&scene=23&srcid=&sharer_sharetime=1573976629730&sharer_shareid=72cab1261a060840685133c77aeb4f5f#rd)
