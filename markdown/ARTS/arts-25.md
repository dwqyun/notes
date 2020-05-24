# ARTS第二十五周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[交换数字](https://leetcode-cn.com/problems/swap-numbers-lcci/)

```js
/**
 * @param {number[]} numbers
 * @return {number[]}
 */
var swapNumbers = function(numbers) {
    [numbers[0], numbers[1]] = [numbers[1], numbers[0]];
    return numbers;
};
```

## Review

[How the Vue Composition API Replaces Vue Mixins | CSS-Tricks](https://css-tricks.com/how-the-Vue-composition-api-replaces-vue-mixins/)

## Tip

- white-space处理元素中的空白符、制表符及换行符，使用pre标签渲染带有回车符或\n时可以使用white-space: pre-line;保留换行且合并空格，结合overflow-wrap: break-word;使行内无法容纳某单词到结尾的，强制分割过长单词换行，效果同word-wrap:break-word;。
- RTL控制符号方向时需要使用方向控制符，left-to-right mark: &lrm; or &#x200e; (U+200E)，right-to-left mark: &rlm; or &#x200f; (U+200F)。

## Share

[CSS3+js实现多彩炫酷旋转圆环时钟效果 " 张鑫旭-鑫空间-鑫生活](https://www.zhangxinxu.com/wordpress/2010/08/css3js%e5%ae%9e%e7%8e%b0%e5%a4%9a%e5%bd%a9%e7%82%ab%e9%85%b7%e6%97%8b%e8%bd%ac%e5%9c%86%e7%8e%af%e6%97%b6%e9%92%9f%e6%95%88%e6%9e%9c/)
