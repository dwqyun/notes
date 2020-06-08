# ARTS第三十一周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[零矩阵](https://leetcode-cn.com/problems/zero-matrix-lcci/)

```js
/*
编写一种算法，若M × N矩阵中某个元素为0，则将其所在的行与列清零。
示例：

输入：
[
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]
输出：
[
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]
*/
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var setZeroes = function (matrix) {
  const m = matrix.length;
  const n = matrix[0].length;
  const rowSet = new Set();
  const colSet = new Set();

  // 先标记需要置0的行列
  for (let i = 0; i < m; i++) {
    for (let j = 0; j < n; j++) {
      if (matrix[i][j] === 0) {
        rowSet.add(i);
        colSet.add(j);
      }
    }
  }

  // 再循环置0
  for (let i = 0; i < m; i++) {
    if (rowSet.has(i)) {
      matrix[i] = Array(n).fill(0);
    }
    for (let j = 0; j < n; j++) {
      if (colSet.has(j)) {
        matrix[i][j] = 0;
      }
    }
  }
};
```

## Review

[await vs return vs return await](https://jakearchibald.com/2017/await-vs-return-vs-return-await/)

## Tip

- JavaScript语句分为普通语句和声明语句，声明型语句跟普通语句最大区别是声明型语句响应预处理过程，普通语句只有执行过程
  - 语句块即大括号`{}`，会产生块级作用域
  - 空语句即分号`;`
  - if语句，if-else条件语句用于少量分支条件判断
  - switch语句，略快于if语句，多分支时应该考虑使用Objective/Map数据集合
  - 循环语句  
      for循环，分三块，先声明索引和数组长度局部变量，满足前置条件后执行语句，再增减索引值，下一次循环又一次判断是否满足条件...
      for in循环，枚举对象的实例和原型链属性(enumerable 为true)，使用hasOwnProperty判断是否实例属性
      for of循环，使用Symbol.iterator方法遍历成员，支持遍历器的数据结构有Array、Map、Set、String、Generator 对象及类数组(arguments、NodeList)
      for await of循环，等待表达式执行结构，支持异步生成器函数
      while循环，前置条件满足则循环
      do-while，后置条件循环，先执行一次再判断条件，至少执行一次
  - return语句，终止函数执行返回表达式结果，可终止函数内的if、for/while、switch控制语句，对Array.forEach回调函数使用return无法跳出循环
  - break语句，用于跳出循环语句或switch 语句，支持跳出到指定标签语句
  - continue语句，用于结束本次循环并继续循环，支持跳出到指定标签语句
  - with语句，将传入的对象推入到作用域链首位，with语句内局部变量会先从传入的对象检索；与try-catch语句的catch字句类似，将异常对象置顶于作用域链
  - throw语句，用于抛出异常
  - try-catch语句，用于捕获异常可配合throw语句使用，try 标识捕获异常的代码块，catch 用于捕获异常后处置，finally 则用于执行一些必须的任务(即使在try 语句中执行return，finally 中的语句也一定执行)
  - debugger语句，通知调试器在此断点
  - var语句，会出现变量提升，变量声明尽可能初始化、就近使用处声明、扎堆声明多个变量
  - let语句，支持块作用域，不存在变量提升，声明前不可使用出现暂时性死区，不能重复声明
  - const语句，与let特性一致，区别在于const声明变量即刻初始化且变量指向的内存地址所保存的数据不能修改
  - class声明，使用class 关键字、名称和一对大括号，声明跟 let 类似，作用于块级作用域，预处理阶段则会屏蔽外部变量
  - import声明，接受一对大括号指定要从其他模块导入的变量名，可使用as关键字重命名，变量是模块的引用，类似const只读，静态编译会将变量提升至模块头部
  - 函数声明
    普通函数声明，使用 function 关键字
    async函数声明
    generator函数声明
    async generator函数声明

## Share

[移动前端开发和 Web 前端开发的区别是什么？](https://mp.weixin.qq.com/s/kPn-2y3Q_CMjwCB1c1yVTA)
