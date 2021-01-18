# ARTS第五十九周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[消失的两个数字](https://leetcode-cn.com/problems/missing-two-lcci/)

```js
/* 
给定一个数组，包含从 1 到 N 所有的整数，但其中缺了两个数字。你能在 O(N) 时间内只用 O(1) 的空间找到它们吗？

以任意顺序返回这两个数字均可。

示例 1:

输入: [1]
输出: [2,3]
示例 2:

输入: [2,3]
输出: [1,4]
提示：

nums.length <= 30000
*/

/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var missingTwo = function (nums) {
  const n = nums.length + 2;
  // 求 a + b 和:  1+2+...+n = n*(n + 1)/2
  const sum = nums.reduce((pre, cur) => pre + cur);
  const sumAB = n * (n + 1) / 2 - sum;
  // 中位数 先找到一个缺失的数 再找第二个数
  const limit = Number.parseInt(sumAB / 2);
  // 对小于等于limit元素求和 1+..+limit - sumLimit = a，得到第一个缺失的数
  const sumLimit = nums.reduce((pre, cur) => (cur <= limit) ? (pre + cur) : pre, 0);
  const a = limit * (limit + 1) / 2 - sumLimit;
  return [a, sumAB - a];
};
```

## Review

[JavaScript Concurrency Models: The Event Loop](https://hackernoon.com/javascript-concurrency-models-the-event-loop-kj2b31ar)

## Tip

- Cross-Site Scripting(跨站脚本攻击)简称为XSS，是攻击者注入恶意脚本并使其在用户终端上执行，窃取用户数据或冒充用户请求
  - 存储型XSS，是恶意代码存储到数据库由服务端返回给浏览器时解析执行，如拼接HTML渲染用户发表内容产生注入
  - 反射型XSS，构造包含恶意代码的URL，服务端将URL返回给浏览器输出到页面，用户点击链接时被执行，常出现于URL传参功能
  - DOM型XSS，用户打开带恶意代码URL，用户浏览器解析执行，属于JS前端漏洞，前两者属于服务端漏洞，DOM型问题如取URL参数直接用于页面加载显示导致恶意基本执行
  - 预防
    - 输入过滤，前端权衡限定用户输入最小类型、内容长度，后端对明确需要过滤的类型进行转义安全化，以及服务端安全请求头设置
    - 输出校验，不可信的数据输出到页面主要靠前端对HTML注入和JavaScript执行做校验转义，攻击发生在前端
      - 涉及HTML属性值value/href/src、标签内容innerHTML、内联事件/style/script代码、DOM节点操作append等注意不可信数据校验，优先使用textContent、setAttribute、addEventListener，对属性值做safeAttribute操作如校验href/src是否包含JavaScript:/data:，对跳转类属性值使用使用正则或白名单检测scheme协议、是否包含特殊字符、URL参数值是否符合设定规则
      - 使用框架库注意v-html/dangerousSetInnerHTML功能，考虑引入第三方XSS校验库，设定HTML标签、属性白名单
      - JS中的eval/setTimeout/setInterval/new Function都可将字符串作为代码运行，避免使用或校验不可信数据

```js
/* 来自 https://github.com/leizongmin/js-xss  可用于富文本/markdown等HTML片段校验*/
/* 对属性值安全校验有 safeAttrValue ，转义有 escapeHtml、escapeAttrValue  */
var source = "<strong>hello</strong><script>alert(/xss/);</script>end";
var html = xss(source, {
  whiteList: [], // empty, means filter out all tags
  stripIgnoreTag: true, // filter out all HTML not in the whitelist
  stripIgnoreTagBody: ["script"] // the script tag is a special case, we need
  // to filter out its content
});

/((j\s*a\s*v\s*a|v\s*b|l\s*i\s*v\s*e)\s*s\s*c\s*r\s*i\s*p\s*t\s*|m\s*o\s*c\s*h\s*a)\:/gi.test('javascript:alert("xss")')
/(^https:)|(^mailto:)|(^tel:)/.test(href);
```

## Share

[V8 引擎垃圾回收与内存分配](https://mp.weixin.qq.com/s/2ARruErg3xNlvPOYjw7IiA)
