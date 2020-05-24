# ARTS第二周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[寻找两个正序数组的中位数](https://leetcode-cn.com/explore/interview/card/tencent/221/array-and-strings/895/)

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number}
 */
var findMedianSortedArrays = function(nums1, nums2) {
    let arr = [...nums1, ...nums2].sort((a,b) => a - b);
    let len = arr.length;
    if (arr.length % 2) {
        return arr[(len - 1) / 2];
    }
    else {
        return (arr[len / 2] + arr[len / 2 - 1]) / 2;
    }
};
```

## Review

[Using Array reduce](https://davidwalsh.name/using-array-reduce)

> reduce为数组中的每一个元素依次执行callback函数，不包括数组中被删除或从未被赋值的元素，接受四个参数：  
`accumulator` 累计器  
`currentValue` 当前值  
`currentIndex` 当前索引  
`array` 数组  
> 回调函数第一次执行时，accumulator 和currentValue的取值有两种情况：如果调用reduce()时提供了`initialValue`，accumulator取值为initialValue，currentValue取数组中的第一个值；如果没有提供 initialValue，那么accumulator取数组中的第一个值，currentValue取数组中的第二个值。
> 注意：如果没有提供initialValue，reduce 会从索引1的地方开始执行 callback 方法，跳过第一个索引。如果提供initialValue，从索引0开始。

## Tip

- 在一元素和当前浏览位置做scrollTop切换时，需要在onScroll监听中记录当前scrollTop值，在触发回滚指定元素时用另一临时变量缓存当前scrollTop值，并使用element.scrollIntoView滚动到这一元素，触发回滚之前浏览位置则使用scrollTo滚动，若需要平滑滚动则需要在scrollIntoView/scrollTo添加额外参数或在滚动元素上添加样式scroll-behavior: smooth;
- 使用video获取视频链接第一帧，需要在赋值src前需要将crossOrigin设为anonymous便于canvas跨域获取视频链接的第一帧：

```js
let video = document.createElement('VIDEO');
video.crossOrigin = 'anonymous';
// TODO: 赋值视频链接
video.src = targetSrc;
video.onloadeddata = () => {
  let canvas = document.createElement('canvas');
  canvas.width = video.videoWidth;
  canvas.height = video.videoHeight;
  canvas.getContext('2d').drawImage(video, 0, 0, canvas.width, canvas.height);
  let imgSrc = canvas.toDataURL('image/png', 0.5);
  console.log('0.5 quality video first frame: ', imgSrc);
  video = null;
}
```

## Share

[【PPT】张鑫旭：工作10年，我在前端专业成长路上的探索](https://mp.weixin.qq.com/s/mjzhU4K-RS6IbhBiiL0sgw)
