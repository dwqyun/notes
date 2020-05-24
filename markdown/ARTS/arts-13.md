# ARTS第十三周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[除自身以外数组的乘积](https://leetcode-cn.com/problems/product-of-array-except-self/)

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function(nums) {
  return nums.map((val, i) => {
    return nums.reduce((sum, value, index) => i !== index ? value * sum : sum, 1);
  });
};
```

## Review

[15 Common Operations on Arrays in JavaScript (Cheatsheet)](https://dmitripavlutin.com/operations-on-arrays-javascript/)

## Tip

- 任何运算的操作数总是从左到右计算的；表达式作左操作数则是引用，作右操作数则是取值；引用不被任何变量持有时则被销毁，也就无法访问其值。
- 宿主环境中，undefined是一个全局属性(只读)，而null是一个关键字。
- export只会导出名字(标识符)和值(字面量)，导出值时需要一个缺省的名字default；名字“default”只是被初始化为一个“单次绑定的、未初始化的标识符”,export default function() {}并不是导出了一个匿名函数表达式，而是导出了一个匿名函数定义；在处理 export/import 语句的全程，没有表达式被执行，import 构建依赖树时名字已经存在于模块最顶层代码，给名字绑定值模块的装配过程，就是执行一次顶层代码。

## Share

[高效程序员的6个习惯](https://mp.weixin.qq.com/s/XEa6eUo5IPEgH_5l2ReuAA)
