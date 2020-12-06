# ARTS第五十四周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[煎饼排序](https://leetcode-cn.com/problems/pancake-sorting/)

```js
/* 煎饼排序
给定数组 A，我们可以对其进行煎饼翻转：我们选择一些正整数 k <= A.length，然后反转 A 的前 k 个元素的顺序。我们要执行零次或多次煎饼翻转（按顺序一次接一次地进行）以完成对数组 A 的排序。

返回能使 A 排序的煎饼翻转操作所对应的 k 值序列。任何将数组排序且翻转次数在 10 * A.length 范围内的有效答案都将被判断为正确。

 

示例 1：

输入：[3,2,4,1]
输出：[4,2,4,3]
解释：
我们执行 4 次煎饼翻转，k 值分别为 4，2，4，和 3。
初始状态 A = [3, 2, 4, 1]
第一次翻转后 (k=4): A = [1, 4, 2, 3]
第二次翻转后 (k=2): A = [4, 1, 2, 3]
第三次翻转后 (k=4): A = [3, 2, 1, 4]
第四次翻转后 (k=3): A = [1, 2, 3, 4]，此时已完成排序。 
示例 2：

输入：[1,2,3]
输出：[]
解释：
输入已经排序，因此不需要翻转任何内容。
请注意，其他可能的答案，如[3，3]，也将被接受。
 

提示：

1 <= A.length <= 100
A[i] 是 [1, 2, ..., A.length] 的排列 */
/**
 * @param {number[]} arr
 * @return {number[]}
 */
var pancakeSort = function (arr) {
  const len = arr.length;
  let res = [];
  const getMaxIndex = (endIndex) => {
    let maxIndex = 0;
    for (let i = 0; i < endIndex; i++) {
      if (arr[i] > arr[maxIndex]) {
        maxIndex = i;
      }
    }

    return maxIndex;
  }

  for (let i = len - 1; i > 0; i--) {
    const j = getMaxIndex(i + 1);
    // 将最大数移动到头部
    if (j > 0) {
      arr.splice(0, j + 1, ...arr.slice(0, j + 1).reverse());
      res.push(j + 1);
    }
    // 再将最大数移动到当前区间尾部
    arr.splice(0, i + 1, ...arr.slice(0, i + 1).reverse());
    res.push(i + 1);
  }

  return res;
};
```

## Review

[ES Modules in Depth](https://ui.dev/esmodules/)

## Tip

- DOM API切换布尔属性值通常是`setAttribute` + `removeAttribute`，新增的[`toggleAttribute`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/toggleAttribute)支持切换元素布尔值属性的状态（属性不存在则添加，存在则移除），语法为`Element.toggleAttribute(name [, force]);`

```js
// force可选参数为强制设置值，返回值hasAttribute为true则表示添加属性
const hasAttribute = ele.toggleAttribute(name, true);

// MDN Polyfill

if (!Element.prototype.toggleAttribute) {
  Element.prototype.toggleAttribute = function(name, force) {
    if(force !== void 0) force = !!force

    if (this.getAttribute(name) !== null) {
      if (force) return true;

      this.removeAttribute(name);
      return false;
    } else {
      if (force === false) return false;

      this.setAttribute(name, "");
      return true;
    }
  };
}
```

## Share

[编写高质量可维护的代码：组件的抽象与粒度](https://mp.weixin.qq.com/s/6U8zMpnBk9nBI_bQAobdfw)
