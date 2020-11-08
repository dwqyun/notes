# ARTS第五十周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[数组中的逆序对](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

```js
/*  数组中的逆序对
在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。
示例 1:

输入: [7,5,6,4]
输出: 5

限制：

0 <= 数组长度 <= 50000 */
/**
 * @param {number[]} nums
 * @return {number}
 */
var reversePairs = function (nums) {
  // 归并
  function mergeSort(nums) {
    const len = nums.length;

    if (len < 2) { return nums };

    const mid = parseInt(len / 2);
    let left = nums.slice(0, mid);
    let right = nums.slice(mid);

    return merge(mergeSort(left), mergeSort(right));
  }

  function merge(left, right) {
    let res = [];
    let leftLen = left.length;
    let rightLen = right.length;
    let len = leftLen + rightLen;

    for (let index = 0, i = 0, j = 0; index < len; index++) {
      if (i >= leftLen) { res[index] = right[j++]; }
      else if (j >= rightLen) { res[index] = left[i++]; }
      else if (left[i] <= right[j]) { res[index] = left[i++]; }
      else {
        res[index] = right[j++];
        count += leftLen - i;
      }
    }

    return res;
  }

  let count = 0;

  mergeSort(nums);

  return count;
};
```

## Review

[Full-Bleed Layout Using CSS Grid](https://joshwcomeau.com/css/full-bleed/)

## Tip

- CSS实现图标变色方案，一是filter的[drop-shadow()](https://developer.mozilla.org/zh-CN/docs/Web/CSS/filter-function/drop-shadow)，投影是原图非透明部分用指定颜色绘制合成在原图像下，Chrome下需要配合透明边框使用，在移动端兼容性还不够良好；二是CSS3 mask遮罩， 跟filter类似需要图片支持透明，目标图标颜色基于非透明区域显示，属性设置类似background；三是background-blend-mode混合模式，需要限定图标为纯黑或纯白；四是兼容性良好的SVG，配合fill、color控制颜色；PNG图片使用mask方案在移动端兼容性和写法为最佳，Chrome下都需要添加-webkit-前缀，mask-image和background-color分开书写，不用mask简写避免兼容性问题

```css
/* 参考 https://www.zhangxinxu.com/wordpress/2018/11/css-change-icon-color/ */

/* 黑 */
filter: brightness(0);
/* 白 */
filter: brightness(100);
/* 投影指定颜色 */
filter: drop-shadow(12px rgba(0, 0, 0, 0.6));

/* mask */
.mask-icon {
    display: inline-block;
    width: 24px;
    height: 24px;
    background-color: rgba(0, 0, 0, 0.6);
    -webkit-mask-image: url(https://mdn.mozillademos.org/files/12676/star.svg);
    mask-image: url(https://mdn.mozillademos.org/files/12676/star.svg);
    -webkit-mask-repeat: no-repeat;
    mask-repeat: no-repeat;
    -webkit-mask-size: 100% 100%;
    mask-size: 100% 100%;
}
```

## Share

[致敬Vue3: 1.1万字从零解读Vue3.0源码响应式系统](https://mp.weixin.qq.com/s/d2xW9ULiB3JLLmDljyihfA)
