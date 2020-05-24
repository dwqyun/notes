# ARTS第二十一周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[回文数](https://leetcode-cn.com/problems/palindrome-number/)

```js
var isPalindrome = function (x) {
  if (x < 0 || (x !== 0 && x % 10 === 0)) {
    return false;
  }

  if (x < 10) {
    return true;
  }

  let num = 0;

  while (x > num) {
    num = num * 10 + x % 10;
    if (x === num) {
      return true;
    }
    x = parseInt(x / 10, 10);
  }
  return x === num || x === num / 10;
};
```

## Review

[Hiding Content for Accessibility](https://snook.ca/archives/html_and_css/hiding-content-for-accessibility)

## Tip

- H5唤醒APP方式主要包括scheme和intent，scheme使用iframe标签src属性询问拉起，需要结合setTimeout和onvisibilitychange判断是否成功拉起再决定是否跳转失败地址，但不适用于Chrome内核浏览器(包括webview)；Chrome需要使用intent拼接scheme信息直接拉起，不需要询问用户，拉起失败可以配置回调地址。

## Share

[【第1301期】如何阅读大型前端开源项目的源码](https://mp.weixin.qq.com/s?__biz=MjM5MTA1MjAxMQ==&mid=2651228920&idx=2&sn=0dac72bba4e6c46667b0aecfc0d7aac8&chksm=bd49537c8a3eda6a2c62390337560f27e8750879a3900825b74e3b73a119665414e823729c29&scene=21#wechat_redirect)
