# ARTS第五十一周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[布尔运算](https://leetcode-cn.com/problems/boolean-evaluation-lcci/)

```js
/*
布尔运算
给定一个布尔表达式和一个期望的布尔结果 result，布尔表达式由 0 (false)、1 (true)、& (AND)、 | (OR) 和 ^ (XOR) 符号组成。实现一个函数，算出有几种可使该表达式得出 result 值的括号方法。

示例 1:

输入: s = "1^0|0|1", result = 0

输出: 2
解释: 两种可能的括号方法是
1^(0|(0|1))
1^((0|0)|1)
示例 2:

输入: s = "0&0&0&1^1|0", result = 1

输出: 10
提示：

运算符的数量不超过 19 个
*/
/**
 * @param {string} s
 * @param {number} result
 * @return {number}
 */
var countEval = function (s, result) {
  const arr = [...s];
  const len = arr.length;
  const dp = [];
  for (let i = 0; i < len; i++) {
    dp[i] = [];
    for (let j = 0; j < len; j++) {
      dp[i][j] = [-1, -1];
    }
  }


  // 计算布尔值
  const getBooleanResult = function (val1, val2, operator) {
    switch (operator) {
      case '^':
        return val1 ^ val2;
      case '|':
        return val1 | val2;
      case '&':
      default:
        return val1 & val2;
    }
  }

  // 返回从索引start到end值为result的不同括号方案的个数
  const rec = function (start, end, result) {
    if (start === end) {
      return Number(arr[start] == result);
    }

    if (dp[start][end][result] !== -1) {
      return dp[start][end][result];
    }

    let ansCount = 0;
    // 索引k划分[s, k] 和 [k + 2, e]，k+1值为运算符，结果组合为{00, 01, 10, 11} 等于result则方案相乘增加
    for (let k = start; k < end; k += 2) {
      const operator = arr[k + 1];
      for (let i = 0; i <= 1; i++) {
        for (let j = 0; j <= 1; j++) {
          if (getBooleanResult(i, j, operator) == result) {
            ansCount += rec(start, k, i) * rec(k + 2, end, j);
          }
        }
      }
    }

    dp[start][end][result] = ansCount;
    return ansCount;
  }

  return rec(0, len - 1, result);
};
```

## Review

[Why do you need to know about Array-like Objects?](https://blog.greenroots.info/why-do-you-need-to-know-about-array-like-objects-ckgsynazh07er06s18ppn32n0)

- 类数组arguments、NodeList、HTMLCollection可以使用for of循环遍历，或使用`Array.prototype.slice.call(arguments)`、`[]...arguments]`、`Array.from(arguments)`转为数组
- NodeList为元素快照(如 DOM querySelectorAll 返回)，HTMLCollection为关联DOM的动态集合(如 DOM getElementByClassName 返回)，应该注意缓存HTMLCollection 长度及拷贝数组减少访问DOM

## Tip

- 实现subTab组件时，可以使用`activeTabElement.scrollIntoView()({inline: "center", behavior: "smooth"})`使激活项移动到中间加上smooth参数或设置样式添加平滑滚动效果，若需要指定滑动动画曲线和滑动完成后执行回调，则需要计算tab移动到中间所需要的scrollLeft值，再滑动动画时间函数内分段给滚动元素赋值scrollLeft

```html
<div role="tablist" class="tab-list">
  <div role="tab" class="list-item active" aria-selected="true" tabindex="0"></div>
  ...
  <div role="tab" class="list-item" aria-selected="false" tabindex="1"></div>
</div>
```

```css
/* 使用 smooth 平滑滚动则分段函数指定时间改变scrollTop/scrollLeft不生效 */
.tab-list {
  overflow-x: scroll;
  scroll-behavior: smooth;
}
```

```js
const tabScrollBox = document.querySelector('.tab-list');
const activeTabElement = document.querySelector('.list-item.active');
const { offsetLeft, offsetWidth } = activeTabElement;
const { offsetWidth: scrollBoxWidth, scrollLeft } = tabScrollBox;
// 位移值
const posX = offsetLeft + offsetWidth / 2 - scrollBoxWidth / 2;

/**
 * 横纵向滚动 参考ivew scrollTop方法(https://github.com/iview/iview/blob/2.0/src/utils/assist.js)
 *
 * @param {滚动参数} { el, from = 0, to = 0, isHorizontal = false, duration = 300 }
 * @return {Promise}
 */
const scrollToCenter = ({ el, from = 0, to = 0, isHorizontal = false, duration = 300 }) => {
  return new Promise((resolve, reject) => {
    if (!(el instanceof HTMLElement)) {
      return reject();
    }

    if (!window.requestAnimationFrame) {
      window.requestAnimationFrame = (
        window.webkitRequestAnimationFrame ||
        window.mozRequestAnimationFrame ||
        window.msRequestAnimationFrame ||
        function (callback) {
          return window.setTimeout(callback, 1000 / 60);
        }
      );
    }
    const difference = Math.abs(from - to);
    const step = Math.ceil(difference / duration * 50);

    function scroll(start, end, step) {
      if (start === end) {
        return resolve();
      }

      let d = (start + step > end) ? end : start + step;
      if (start > end) {
        d = (start - step < end) ? end : start - step;
      }

      if (isHorizontal) {
        el.scrollLeft = d;
      } else {
        el.scrollTop = d;
      }
      window.requestAnimationFrame(() => scroll(d, end, step));
    }
    scroll(from, to, step);
  });
}

scrollToCenter({ el: tabScrollBox, from: scrollLeft, to: posX, isHorizontal: true, duration: 300 }).then(() => {
  console.log('scrollToCenter');
});
```

## Share

[77.9K 的 Axios 项目有哪些值得借鉴的地方](https://mp.weixin.qq.com/s/gqr-CpLEIAEymbdLX3NrpQ)
