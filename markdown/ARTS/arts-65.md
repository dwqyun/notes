# ARTS第六十五周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[四数相加 II](https://leetcode-cn.com/problems/4sum-ii/)

```js
/* 
给定四个包含整数的数组列表 A , B , C , D ,计算有多少个元组 (i, j, k, l) ，使得 A[i] + B[j] + C[k] + D[l] = 0。

为了使问题简单化，所有的 A, B, C, D 具有相同的长度 N，且 0 ≤ N ≤ 500 。所有整数的范围在 -228 到 228 - 1 之间，最终结果不会超过 231 - 1 。

例如:

输入:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

输出:
2

解释:
两个元组如下:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
*/

/**
 * @param {number[]} A
 * @param {number[]} B
 * @param {number[]} C
 * @param {number[]} D
 * @return {number}
 */
var fourSumCount = function (A, B, C, D) {
  // 计算 AB两数和为key sumAB值出现次数为value 存入Map；再计算CD中两数之和相反数是否在Map中
  const countAB = new Map();
  let count = 0;

  for (const a of A) {
    for (const b of B) {
      const sumAB = a + b;
      countAB.set(sumAB, countAB.has(sumAB) ?  countAB.get(sumAB) + 1 : 1);
    }
  }

  for (const c of C) {
    for (const d of D) {
      const sumCD = -c - d;
      countAB.has(sumCD) && (count += countAB.get(sumCD)) ;
    }
  }

  return count;
};
```

## Review

[An Interactive Guide to CSS Transitions](https://2ality.com/2020/09/ecmascript-2021.html)

## Tip

- 跨源资源共享 [CORS](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS)
  - 浏览器出于安全性会限制跨源HTTP请求，浏览器通过response或预检请求检测响应报文是否包含正确的CORS响应头，从而使跨源数据安全传输，CORS请求是包含origin首部字段的HTTP请求，`Access-Control-Request-Method`、`Access-Control-Request-Headers`和`Origin`是跨源请求时自动携带的，将实际请求的HTTP方法、携带的首部字段、源站标识给服务器
  - 解决CORS问题
    - 后端设置 `Access-Control-Allow-Origin`，标识浏览器服务端允许的跨源请求，如果有多个跨源站应该使用白名单校验请求头Origin字段
    - 使用 代理服务器(Proxy server)， 脱离浏览器同源策略限制，适用于请求第三方资源，Proxy加上CORS header解决前端请求被阻挡问题
    - 后端提供 JSONP支持，只支持get请求，利用script标签可跨域特性结合后端动态返回回调方法
  - 如果需要检验前端请求是否在后端预期之内，符合预期后则响应正式请求，则应该使用非简单请求，会触发预检请求(preflight request)，只要method是GET、POST或是HEAD然后不要带自订的header，Content-Type也不要超出：application/x-www-form-urlencoded、multipart/form-data或是text/plain这三种，需要后端设定`Access-Control-Request-Headers`、`Access-Control-Request-Method`指示响应的URL支持的HTTP方法、字段
  - request若需要携带身份凭证需要将 withCredentials 标志设置为 true(fetch则是设置credentials: 'include')，后端则需要设定`Access-Control-Allow-Credentials: true`，且不能设置 `Access-Control-Allow-Origin` 的值为`*`
  - 浏览器通过getResponseHeader访问非常规响应头,读取自定义header时需要后端设置白名单`Access-Control-Expose-Headers: X-My-Custom-Header, X-Another-Custom-Header`
  - `Access-Control-Max-Age: 86400`可指定preflight请求结果缓存时间，浏览器默认维护一个最大有效时间，有效时间内同一请求不需要再次发起预检请求
  - 若服务器只对带origin的请求返回`Access-Control-Allow-Origin`，那么通过IMG标签响应时不带头，通过JS([canvas绘制场景](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_enabled_image))获取时是CORS请求，但浏览器会直接使用IMG来源的未过期的URL响应缓存，则会出现CORS验证失败，可以通过`Vary: Origin`可设定Origin不同时则重新发起请求

## Share

[【第2236期】CORS完全手册之收官篇](https://mp.weixin.qq.com/s/Ud_3zOoVDxn4Q_zKsbEhrg)
