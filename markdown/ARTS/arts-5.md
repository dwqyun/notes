# ARTS第五周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[最长公共前缀](https://leetcode-cn.com/explore/interview/card/tencent/221/array-and-strings/898/)

```js
/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function (strs) {
  if (strs.length === 0 || strs.length === 1) {
    return strs[0] || '';
  }
  let maxIndex = strs[0].length;
  let index = 1;
  let commonPrefix = '';
  while (index < strs.length) {
    commonPrefix = strs[0].substring(0, maxIndex);
    if (!strs[index].startsWith(commonPrefix)) {
      index > 1 && index--;
      maxIndex--;
    } else {
      index++;
    }
  }
  return commonPrefix;
};
```

## Review

[Level up your .sort game | CSS-Tricks](https://css-tricks.com/level-up-your-sort-game/)

- sort结合...扩展运算符、localeCompare 、Math.random()等结合应用

## Tip

- window.name可读可写，只支持字符串，只能用于当前窗口应用场景有限
- Intl对象是ECMAScript国际化API的命名空间，它提供对语言敏感的字符串比较、支持数字格式化以及日期和时间的格式化。Intl.Collator可支持对语言敏感的字符串比较,new Intl.DateTimeFormat([locales[, options]])格式化时间，Intl.ListFormat可以让对语言敏感的列表进行格式化，Intl.NumberFormat可以根据不同语言环境最数值字符串（位数补0、金额、星期、千位分隔符）进行不同的呈现处理，张鑫旭的文章中还有有详细介绍连续数字千位分隔。

```js
/**
 * @param {array} letters
 * @param {string} lang
 * @param {object} options
 * @return {string}
 */
function letterSort(letters, lang, options = {}) {
  return letters.sort(new Intl.Collator(lang, options).compare);
}
letterSort(["胡歌", "井柏然", "刘烨", "陈坤"], 'zh', {});
letterSort(['15', '2', '100'], 'kn', { numeric: true });


new Intl.DateTimeFormat('zh', {
    year: 'numeric',  
    month: '2-digit',
    day: '2-digit',
    hour: '2-digit',
    minute: '2-digit',
    second: '2-digit',
    hour12: false
}).format(new Date())
```

## Share

[JS Intl对象完整简介及在中文中的应用](https://www.zhangxinxu.com/wordpress/2019/09/js-intl-zh/)
