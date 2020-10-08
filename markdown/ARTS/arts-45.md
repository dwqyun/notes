# ARTS第四十五周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)

```js
/* 丑数
我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
说明:  

1 是丑数。
n 不超过1690。 */
/**
 * @param {number} n
 * @return {number}
 */
var nthUglyNumber = function (n) {
  const res = new Array(n).fill(1);
  let p2 = 0, p3 = 0, p5 = 0;

  for (let i = 1; i < n; i++) {
    // 2 3 5 组成的三个丑数相乘值数组中按最小值排序赋值
    res[i] = Math.min(res[p2] * 2, res[p3] * 3, res[p5] * 5);
    // 1*2 2*2 3*2...
    if (res[i] === res[p2] * 2) {
      p2++;
    }
    // 1*3 2*3 3*3...
    if (res[i] === res[p3] * 3) {
      p3++;
    }
    // 1*5 2*5 3*5...
    if (res[i] === res[p5] * 5) {
      p5++;
    }
  }

  return res[n - 1];
};
```

## Review

[How to Create an Async Function via “new Function”](https://davidwalsh.name/async-function-class)

## Tip

- CSS滤镜和混合模式处理图下载，可以使用SVG foreignObject元素包裹HTML和CSS代码，再作为img标签显示后使用canvas截取图片，最后动态创建a标签+download+click触发下载
- Symbol是一种原生数据类型，设计目的是作为对象属性的唯一标识符，防止对象属性冲突，可做对象私有属性访问控制，可显性转换为字符串和布尔值，但不能转数值，for-in、JSON.stringify、Object.keys、Object.getOwnPropertyNames会忽略symbol作为键的属性，使用new Symbol()创建包装器对象不被支持，创建Symbol包装器对象可以使用Object()函数包装

```js
typeof Symbol(); // symbol
new Symbol(); // Uncaught TypeError: Symbol is not a constructor
const description = Symbol('description');
const symObj = Object(description);
typeof symObj;  // object

//Symbol([description]) description为可选参数 调用Symbol()函数动态匿名生成一个唯一的值 通过Object.getOwnPropertySymbols()遍历获取
var  myPrivateMethod  = Symbol();
this[myPrivateMethod] = function() {...};
```

## Share

[CSS 属性选择器深入挖掘](https://mp.weixin.qq.com/s/GQeWsojO57Uik5bGWa9Nbg)
