# ARTS第六十四周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[寻找重复数](https://leetcode-cn.com/problems/find-the-duplicate-number/)

```js
/* 
给定一个包含 n + 1 个整数的数组 nums ，其数字都在 1 到 n 之间（包括 1 和 n），可知至少存在一个重复的整数。

假设 nums 只有 一个重复的整数 ，找出 这个重复的数 。

 

示例 1：

输入：nums = [1,3,4,2,2]
输出：2
示例 2：

输入：nums = [3,1,3,4,2]
输出：3
示例 3：

输入：nums = [1,1]
输出：1
示例 4：

输入：nums = [1,1,2]
输出：1
 

提示：

2 <= n <= 3 * 104
nums.length == n + 1
1 <= nums[i] <= n
nums 中 只有一个整数 出现 两次或多次 ，其余整数均只出现 一次
*/

/**
 * @param {number[]} nums
 * @return {number}
 */
var findDuplicate = function (nums) {
  const len = nums.length;
  const uniqueArr = [... new Set(nums)];
  const uniqueLen = uniqueArr.length;
  const sum = nums.reduce((pre, cur) => pre + cur, 0);
  const sumUnique = uniqueArr.reduce((pre, cur) => pre + cur, 0);

  return (sum - sumUnique) / (len - uniqueLen);
};
```

## Review

[I DON'T WANT TO DO FRONT-END ANYMORE](https://soynomm.com/blog/i-dont-want-to-do-frontend-anymore/)

## Tip

- HTTP重定向状态码区分，3xx状态码表示客户端请求资源出现变化，须用新URI重新请求获取资源
  - `301 Moved Permanently`(永久重定向)，此次请求的资源已被移动到`Location`头部上
  - `302 Found`(临时重定向)， 和 301 都会在响应头`Location 指明浏览器后续要跳转的 URI；区别在于语义，浏览器或爬虫看到 301，会优化URI索引，而对302只跳转不做记录
  - `303 See Other`(查看其他)：与类似 302，要求重定向后的请求转为 GET 方法，如使用PUT请求上传文件后返回确认信息
  - `304 Not Modified`(缓存重定向) 用于 If-Modified-Since 等条件请求，表示资源未修改可重定向已到缓存的文件，用于缓存控制
  - `307 Temporary Redirect`(临时重定向)，与类似 302，要求重定向后请求里的方法和实体不变，在响应 GET 或 HEAD 方法时采用 302 状态码，其他使用307更明确、可预测
  - `308 Permanent Redirect`(永久重定向)，与类似 307，不允许重定向后的请求变动，且含有 301 永久重定向的含义
  - 使用重定向跳转，需要理解`临时`和`永久`；资源不可用场景，例如域名/服务器变更、网站改版、系统维护，这些需要用重定向跳转到新的 URI;避免重复场景，将多个网址都定向跳转到一个URI，增加访问入口，或者是权限不足重定向为提升页面；如果是永久性变更则需要使用301通知浏览器和搜索引擎，若在未来时间点可恢复则使用302
  - 使用重定向需要注意性能损耗和循环跳转，重定向机制会导致一个跳转两个请求，尤其站外跳转会有性能损耗，外部重定向时服务器将重定向地址给浏览器跳转，内部重定向是服务器直接返回重新向资源给浏览器地址不变

## Share

[【第2206期】奇怪的知识——位掩码](https://mp.weixin.qq.com/s/zT4dZPYN3vYMRABWkH5SFQ)
