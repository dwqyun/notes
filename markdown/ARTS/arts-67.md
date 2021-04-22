# ARTS第六十七周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

```js
/* 
给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。答案可以按 任意顺序 返回。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

示例 1：

输入：digits = "23"
输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]
示例 2：

输入：digits = ""
输出：[]
示例 3：

输入：digits = "2"
输出：["a","b","c"]
 

提示：

0 <= digits.length <= 4
digits[i] 是范围 ['2', '9'] 的一个数字。
*/

/**
 * @param {string} digits
 * @return {string[]}
 */
var letterCombinations = function (digits) {
  const len = digits.length;
  if (!len) return [];

  const map = new Map([
    ['2', 'abc'],
    ['3', 'def'],
    ['4', 'ghi'],
    ['5', 'jkl'],
    ['6', 'mno'],
    ['7', 'pqrs'],
    ['8', 'tuv'],
    ['9', 'wxyz'],
  ]);
  const res = [];

  res.push('');
  for (let i = 0; i < len; i++) {
    const levelSize = res.length;
    for (let j = 0; j < levelSize; j++) {
      const curStr = res.shift();
      const letters = map.get(digits[i]);
      // 遍历组合
      for (const l of letters) {
        res.push(curStr + l);
      }
    }
  }
  return res;
};
```

## Review

[Sketchy Webcam Filter Effects](https://frontend.horse/articles/sketchy-webcam-filter-effects/)

## Tip

- [::marker CSS伪元素](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::marker)匹配设置了display: list-item的元素或伪元素，例如<li>和<summary>，属性支持修改list item的marker box（项目符号或者数字）的字体、颜色、内容等
  - content属性不设置则默认显示符号`·`圆点或有序数字
  - 普通HTML标签元素要使用::marker伪元素，可设置display为list-item
  - 浏览器刚支持，用于修改项目列表的符号样式渐进增强

```css
/* 参考 https://www.zhangxinxu.com/wordpress/2021/02/css-marker-pseudo-element/ */
ol li::marker,
ul li::marker {
  color: red;
  font-size: 1.5em;
}

/* <div class="list-item-marker">自定义marker伪元素显示内容</div> */
.list-item-marker::marker {
  content: '*';
  transition: color .2s;
}
.list-item-marker:hover::marker {
  color: red;
}
```

## Share

[【第2250期】如何提高CSS性能](https://mp.weixin.qq.com/s/Sc3ksTndrrNSH5wAhtgAaw)
