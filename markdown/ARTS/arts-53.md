# ARTS第五十三周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[找出数组游戏的赢家](https://leetcode-cn.com/problems/find-the-winner-of-an-array-game)

```js
/* 给你一个由 不同 整数组成的整数数组 arr 和一个整数 k 。

每回合游戏都在数组的前两个元素（即 arr[0] 和 arr[1] ）之间进行。比较 arr[0] 与 arr[1] 的大小，较大的整数将会取得这一回合的胜利并保留在位置 0 ，较小的整数移至数组的末尾。当一个整数赢得 k 个连续回合时，游戏结束，该整数就是比赛的 赢家 。

返回赢得比赛的整数。

题目数据 保证 游戏存在赢家。



示例 1：

输入：arr = [2,1,3,5,4,6,7], k = 2
输出：5
解释：一起看一下本场游戏每回合的情况：

因此将进行 4 回合比赛，其中 5 是赢家，因为它连胜 2 回合。
示例 2：

输入：arr = [3,2,1], k = 10
输出：3
解释：3 将会在前 10 个回合中连续获胜。
示例 3：

输入：arr = [1,9,8,2,3,7,6,4,5], k = 7
输出：9
示例 4：

输入：arr = [1,11,22,33,44,55,66,77,88,99], k = 1000000000
输出：99


提示：

2 <= arr.length <= 10^5
1 <= arr[i] <= 10^6
arr 所含的整数 各不相同 。
1 <= k <= 10^9
 */
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number}
 */
var getWinner = function (arr, k) {
  let preVal = Math.max(arr[0], arr[1]);
  // k=1
  if (k === 1) {
    return preVal;
  }
  let count = 1;
  let maxNum = preVal;
  for (let i = 2, len = arr.length; i < len; i++) {
    // k > 1 时总是preVal与arr[i]比较 k > arr.length -1时遍历完则preVal为数组中最大值
    const curVal = arr[i];
    if (preVal > curVal) {
      count++;
      if (count === k) {
        return preVal;
      }
    }
    else {
      preVal = curVal;
      count = 1;
    }
    maxNum = Math.max(maxNum, curVal);
  }

  return maxNum;
};
```

## Review

[Why CSS :focus-within is amazing](https://dev.to/dailydevtips1/why-css-focus-within-is-amazing-27p8)

## Tip

- 页面适配深色模式，可以使用媒体查询[prefers-color-scheme](https://developer.mozilla.org/zh-CN/docs/Web/CSS/@media/prefers-color-scheme)或JS原生的[window.matchMedia()](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/matchMedia)判断，

```js
// 是否支持深色模式 若在APP中可以传递系统深色标记 事件监听添加深色类名适配
const darkMode = window.matchMedia("(prefers-color-scheme: dark)");

if (darkMode) {
 darkMode.matches&& document.body.classList.add('dark');
 darkMode.addEventListener('change', event => {
  event.matches ? document.body.classList.add('dark') :  document.body.classList.remove('dark');
 });
}

```

```css
/* 深色模式 */
@media (prefers-color-scheme: dark) {
  /* img video等不需要反转色调 */
    html, img {
    filter: invert(1) hue-rotate(.5turn);
  }
}
/* 浅色模式 */
@media (prefers-color-scheme: light) {
}
```

## Share

[你不知道的前端异常处理](https://mp.weixin.qq.com/s/Mi_Sh7hsPlrfhlTprBXlUA)
