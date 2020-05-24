# ARTS第二十七周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[字符串压缩](https://leetcode-cn.com/problems/compress-string-lcci/)

```js
/* 字符串压缩。利用字符重复出现的次数，编写一种方法，实现基本的字符串压缩功能。比如，字符串aabcccccaaa会变为a2b1c5a3。若“压缩”后的字符串没有变短，则返回原先的字符串。你可以假设字符串中只包含大小写英文字母（a至z）。 */
/**
 * @param {string} S
 * @return {string}
 */
var compressString = function (S) {
  const strLen = S.length;
  if (!strLen) {
    return '';
  }
  let charCount = 0;
  let char = S[0];
  let newStr = '';
  for (const ch of S) {
    if (char === ch) {
      charCount++;
    }
    else {
      newStr += char + String(charCount);
      char = ch;
      charCount = 1;
    }
  }
  newStr += char + String(charCount);
  return newStr.length >= strLen ? S : newStr;
};
```

## Review

[You might not need switch in JavaScript](https://www.valentinog.com/blog/switch/)

## Tip

- :focus-visible伪类，浏览器认为使用键盘访问触发的元素聚焦才是:focus-visible表示的聚焦，`:focus:not(:focus-visible) { outline: 0; }`即可以去除Chrome下鼠标点击时的outline而保留键盘访问时的outline
- 可选性伪类:required和:optional，可用于实现问卷调查的必选和可选效果，项使用ol和li元素嵌套，li元素使用`display:table`布局，问题文本标签使用`display:table-caption`用于改变元素的上下呈现位置，li元素的序号使用CSS计数器重现序号匹配，:optional伪类和:required伪类结合伪元素标记可行性

## Share

[前端基础篇之CSS世界](https://mp.weixin.qq.com/s/EYNlUqflaMddFJGtKB4Ktg)
