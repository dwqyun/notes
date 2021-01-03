# ARTS第五十二周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[组合总和 III](https://leetcode-cn.com/problems/combination-sum-iii/)

```js
/*
216. 组合总和 III
找出所有相加之和为 n 的 k 个数的组合。组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

说明：

所有数字都是正整数。
解集不能包含重复的组合。
示例 1:

输入: k = 3, n = 7
输出: [[1,2,4]]
示例 2:

输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
 */
/**
 * @param {number} k
 * @param {number} n
 * @return {number[][]}
 */
var combinationSum3 = function (k, n) {
  // 在1-9中 枚举k个数组合总和为n
  const temp = [];
  const res = [];
  const dfs = (start, end, k, sum) => {
    // 判断组合数字个数小于k
    if (temp.length + (end - start + 1) < k || temp.length > k) {
      return;
    }
    // 判断k个数组合总和等于n
    if (temp.length === k && temp.reduce((pre, val) => pre + val, 0) === sum) {
      res.push(temp.slice());
      return;
    }
    temp.push(start);
    dfs(start + 1, end, k, sum);
    temp.pop();
    dfs(start + 1, end, k, sum);
  }

  dfs(1, 9, k, n);
  return res;
};
```

## Review

[10 useful HTML file upload tips for web developers](https://blog.greenroots.info/10-useful-html-file-upload-tips-for-web-developers-ckgetegpf0c7go9s123wvg7bi?guid=none&deviceId=e2fe45eb-ff11-4b20-80fd-3f5cda9d493c)

## Tip

- swiper无障碍可以开启`a11y`选项，slide可设置aria-hidden和tabindex值，slide可设置tabpanel role，分页器可设置tablist

```html
<!-- vue中可使用v-bind动态添加tabindex属性 替代DOM API设置属性操作 -->
<swiper-slide :tabindex="index === activeIndex ? -1 : undefined"></swiper-slide>
```

```js
/* 参见 issues https://github.com/nolimits4web/swiper/issues/3149 */
slideChange() {
  const currentSlideEl = this.slides[this.realIndex];
  // TODO: removeAttribute tabindex + activeIndex 绑定aria-hidden
  currentSlideEl.setAttribute("tabindex", "-1");
  currentSlideEl.focus();
},
```

- `mix-blend-mode:lighten`结合绝对定位可实现文字选中覆盖指定颜色高亮

```css
[type="radio"]:checked::after {
    content: '';
    position: absolute;
    background-color: red;
    mix-blend-mode: lighten;
}
```

## Share

[【第2116期】Vue 3.0 Ref-sugar 提案真的是自寻死路吗？](https://mp.weixin.qq.com/s/7k4skVdCIhTsTdEFmXyYLg)
