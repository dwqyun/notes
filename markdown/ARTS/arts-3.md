# ARTS第三周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[最长回文子串](https://leetcode-cn.com/explore/interview/card/tencent/221/array-and-strings/896/)

```js
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
  let len = s.length;
  if (!len || len === 1) {
    return s || "";
  }
  let strSplit = s.split('').reduce((acc, cur, index) => `${acc}${cur}#`, '#');
  let strLen = strSplit.length;
  let tempArr = [];
  let max = 0;
  let id = 0;
  let longestPalindrome = 1;
  let longestPalindromeStr = s.substring(0, 1);
  for (let i = 0; i < strLen; i++) {
    if (i < max) {
      tempArr[i] = Math.min(tempArr[2 * id - i], max - i);
    } else {
      if (i > max) {
        throw new Error('error');
      }
      tempArr[i] = 1;
    }
    while (i - tempArr[i] >= 0 && i + tempArr[i] < strLen && strSplit.charAt(i - tempArr[i]) === strSplit.charAt(i + tempArr[i])) {
      tempArr[i]++;
    }
    if (i + tempArr[i] > max) {
      max = i + tempArr[i];
      id = i;
    }
    if (tempArr[i] - 1 > longestPalindrome) {
      longestPalindrome = tempArr[i] - 1;
      longestPalindromeStr = strSplit.substring(i - tempArr[i] + 1, i + tempArr[i]).replace(/#/g, '');
    }

  }
  return longestPalindromeStr;
};
```

## Review

[Everything You Need to Know About Date in JavaScript | CSS-Tricks](https://css-tricks.com/everything-you-need-to-know-about-date-in-javascript/)

- 使用getTime比较时间大小
- 使用getFullYear、getMonth、getDate、getHours、getMinutes、getSeconds、getMilliseconds等组合模板字符串或数组显示特定时间格式

## Tip

- momentjs使用diff比较时间差值时可先用isBefore判断处理之前之后如何显示，如之后可显示具体年月日，之前超过一星期也可显示年月日其他显示天、时、分、秒之前，还需要注意接口返回的时间和本地时间的秒内误差。
- Chrome 25+只能使用Android Intent方式唤醒Native，使用userAgent判断版本和特定浏览器后用A标签href拼接Intent信息触发跳转，其他浏览还是保持使用iframe.src跳转。
- Chrome中使用filter:drop-shadow需要主题部分在页面中可见，故在`overflow:hidden;`后可用透明边框显示主体部分及元素非透明区域投影，border-shadow区别于只是盒阴影。

## Share

[【第1712期】HTTP协议理解及服务端与客户端的设计实现](https://mp.weixin.qq.com/s/69EvvR0FHR57QuhDC7bJ8w)
