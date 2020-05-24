# ARTS第六周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[三数之和](https://leetcode-cn.com/problems/3sum/)

```js
var threeSum = function (nums) {
  let result = [];
  const len = nums.length;
  if (!Array.isArray(nums) || len < 3) return result;
  nums.sort((a, b) => a - b);
  for (let i = 0; i < len; i++) {
    if (nums[i] > 0) break;
    //用左右指针指向nums[i]后的两数字nums[L]、nums[R]
    if (i > 0 && nums[i] == nums[i - 1]) continue;
    let L = i + 1;
    let R = len - 1;
    while (L < R) {
      if (nums[R] < 0) break;
      const sum = nums[i] + nums[L] + nums[R];
      if (sum == 0) {
        result.push([nums[i], nums[L], nums[R]]);
        while (L < R && nums[L] == nums[L + 1]) L++;
        while (L < R && nums[R] == nums[R - 1]) R--;
        L++;
        R--;
      }
      else if (sum < 0) L++;
      else if (sum > 0) R--;
    }
  }
  return result;
};
```

## Review

[Breakout Buttons | CSS-Tricks](https://css-tricks.com/breakout-buttons/)

- 当一块区域都可点击时，可以使用button+伪元素去覆盖，而不用牺牲语义用button嵌套其他标签，区域内其他可点击标签可以再使用z-index提升层级。

## Tip

- 注意无障碍适配，如某一图片可点击应该使用alt准确描述，结合ARIA role属性让屏幕阅读器识别为button。
- 音频文件在webpack也可以打包限制大小转换为base64，使用audio标签时用可压缩性高的ogg格式，通过paused判断状态后使用play()方法播放音频。

## Share

[WAI-ARIA无障碍网页应用属性完全展示](https://www.zhangxinxu.com/wordpress/2012/03/wai-aria-%e6%97%a0%e9%9a%9c%e7%a2%8d%e9%98%85%e8%af%bb/)
