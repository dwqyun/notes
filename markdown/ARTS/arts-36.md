# ARTS第三十六周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[珠玑妙算游戏](https://leetcode-cn.com/problems/master-mind-lcci)

```js
/* 珠玑妙算游戏
计算机有4个槽，每个槽放一个球，颜色可能是红色（R）、黄色（Y）、绿色（G）或蓝色（B）。例如，计算机可能有RGGB 4种（槽1为红色，槽2、3为绿色，槽4为蓝色）。作为用户，你试图猜出颜色组合。打个比方，你可能会猜YRGB。要是猜对某个槽的颜色，则算一次“猜中”；要是只猜对颜色但槽位猜错了，则算一次“伪猜中”。注意，“猜中”不能算入“伪猜中”。

给定一种颜色组合solution和一个猜测guess，编写一个方法，返回猜中和伪猜中的次数answer，其中answer[0]为猜中的次数，answer[1]为伪猜中的次数。

示例：

输入： solution="RGBY",guess="GGRR"
输出： [1,1]
解释： 猜中1次，伪猜中1次。
提示：

len(solution) = len(guess) = 4
solution和guess仅包含"R","G","B","Y"这4种字符 */
/**
 * @param {string} solution
 * @param {string} guess
 * @return {number[]}
 */
var masterMind = function (solution, guess) {
  let solutionCount = 0;
  let guessCount = 0;
  const solutionArr = [...solution];
  const guessArr = [...guess];

  for (let i = 0, sLen = solutionArr.length; i < sLen; i++) {
    if (solutionArr[i] === guessArr[i]) {
      solutionCount += 1;
    }
  }
  while (solutionArr.length) {
    const index = guessArr.indexOf(solutionArr.shift());
    if (index !== -1) {
      guessCount += 1
      guessArr.splice(index, 1);
    }
  }
  return [solutionCount, guessCount - solutionCount];
};
```

## Review

[(JavaScript default parameters]<https://kentcdodds.com/blog/javascript-default-parameters>)

## Tip

- Object的访问器属性(`get`、`set`、`enumerable`、`configurable`)用于描述行为，数据属性(`value`、`writable`、`enumerable`、`configurable`)用于描述状态，Getter/setter可用作实际属性值的包装器，以赋予更多行为控制；configurable描述符代表可删除、属性标记可改；读取不存在的属性时捕获错误可以使用访问器属性，或者`Proxy`代理对象操作，需要注意使用`Reflect`转发对象如`get(target, prop, receiver) { return Reflect.get(...arguments); }`，Proxy代理Getter时还可以嵌套返回新的Proxy对象，通过对象使用不同代理多次包装，结合各个方面的功能对其进行装饰

```js
const user = {
  _name: "Guest",
  get name() {
    return this._name;
  },
  privateInfo: {
    nickName: '0'
  }
};
const info = {
  nickName: '1'
}
const privateInfoHandle = {
  get(target, prop) {
    if (prop in target) {
      try {
        return info[prop];
      } catch (error) {
        throw ReferenceError(`${prop} is undefined`);
      }
    }
    throw ReferenceError(`${prop} is undefined`);
  }
}
const userProxy = new Proxy(user, {
  get(target, prop, receiver) {
    if (prop in target) {
      if (target[prop] instanceof Object) {
        return new Proxy(target[prop], privateInfoHandle);
      }
      return Reflect.get(target, prop, receiver);
    }
    throw ReferenceError(`${prop} is undefined`);
  }
});
```

## Share

[CSS变量对JS交互组件开发带来的提升与变革](https://www.zhangxinxu.com/wordpress/2020/07/css-var-improve-components/)
