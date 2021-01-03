# ARTS第五十七周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[布尔运算](https://leetcode-cn.com/problems/boolean-evaluation-lcci/)

```js

```

## Review

[What is the `toJSON()` Function in JavaScript?](http://thecodebarbarian.com/what-is-the-tojson-function-in-javascript.html)

## Tip

- CSS性能优化，CSS样式表根据设备表现形式拆分减少阻塞，将主样式优先下载其他低优先级；`@import`引入样式是阻塞调用如非依赖减少嵌套@import引入，使用link标签拆分引入并行下载；新特性`content-visibility: auto;contain-intrinsic-size: 0 500px;`可用于优化视口之外大量页面元素渲染卡顿的情况
- DOM API的差异，`textContent`优于`innerText`，innerText会保留换行符、无法获取隐藏元素文本、由于回流性能略差；`getAttribute`对比`dataset`无视大小写，data-*设置属性需要中划线连接小写字母，取值需要驼峰命名；`getElementId`(HTML Collection 关联DOM动态更新)相比`querySelector`(NodeList DOM静态快照)更安全，在未知的选择器是否合法情况下getElementId会返回null，querySelector则报错影响JS运行；`append`和`appendChild`区别在于，append可以一次添加多个元素且append字符串时可以自动转义为HTML；

```js
/* 参考 https://www.zhangxinxu.com/wordpress/2020/12/dom-api-diff/ */
dom.append(node1, node2, node3, ...)
document.body.append('', '');
```

## Share

[框架带来了什么？](https://mp.weixin.qq.com/s/AreRWfVb6L7AaJIhSyaQYA)
