# ARTS第十周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[字符串相乘](https://leetcode-cn.com/problems/multiply-strings/)

```js
/**
 * @param {string} num1
 * @param {string} num2
 * @return {string}
 */
var multiply = function(num1, num2) {
  if (num1 === '0' || num2 === '0') {
    return '0';
  }
  const len1 = num1.length;
  const len2 = num2.length;
  let res = new Array(len1 + len2).fill(0);
  for (let i = len2 - 1; i >= 0; i--) {
    for (let j = len1 - 1; j >= 0; j--) {
      const temp = (res[i + j + 1] - '0') + (num1[j] - '0') * (num2[i] - '0');
      res[i + j + 1] = temp % 10;
      res[i + j] += Math.floor(temp / 10);
    }
  }

  for (let i = 0; i < len1 + len2; i++) {
    if (res[i] != 0) {
      return res.splice(i).join('');
    }
  }
  return '0';
};
```

## Review

[Highlights from Chrome Dev Summit 2019](https://bitsofco.de/chrome-dev-summit-2019/)

## Tip

- HTML5响应式图片，背景图片根据屏幕密度可以使用image-set()，IMG标签可使用pictrue、source及属性sizes尺寸、srcset密度资源、type类型。
- window.devicePixelRatio是设备上物理像素和设备独立像素(device-independent pixels (dips))的比例

## Share

[【第1785期】JS与数](https://mp.weixin.qq.com/s/3M96mvdivHQEQZwLjpBd_w)
