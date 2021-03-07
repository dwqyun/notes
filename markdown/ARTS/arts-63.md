# ARTS第六十三周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[组合总和](https://leetcode-cn.com/problems/combination-sum/)

```js
/* 
组合总和
给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的数字可以无限制重复被选取。

说明：

所有数字（包括 target）都是正整数。
解集不能包含重复的组合。 
示例 1：

输入：candidates = [2,3,6,7], target = 7,
所求解集为：
[
  [7],
  [2,2,3]
]
示例 2：

输入：candidates = [2,3,5], target = 8,
所求解集为：
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
 
提示：

1 <= candidates.length <= 30
1 <= candidates[i] <= 200
candidate 中的每个元素都是独一无二的。
1 <= target <= 500
*/
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function (candidates, target) {
  const ans = [];
  // 参考官方解答搜索回溯
  // dfs表示当前在 candidates 数组的第 idx 位，还剩 target 要组合，已经组合的列表为 combine
  const dfs = (target, combine, idx) => {
    // 递归的终止条件为 target <= 0 或者 candidates 数组被全部用完
    if (idx === candidates.length) {
      return;
    }
    if (target === 0) {
      ans.push(combine);
      return;
    }
    // 每次搜索延伸两个分支直至递归终止
    // 直接跳过当前数
    dfs(target, combine, idx + 1);
    // 选择当前数时数字可以重复选取 下标仍为idx
    if (target - candidates[idx] >= 0) {
      // 如在candidates = [2, 3, 6, 7]，target = 7中，已组合列表为[2]，还剩[7 - 2]需要组合，继续递归做减法，以target为根画树形图
      dfs(target - candidates[idx], [...combine, candidates[idx]], idx);
    }
  }

  dfs(target, [], 0);
  return ans;
};
```

## Review

[2020 JavaScript Rising Stars](https://risingstars.js.org/2020/en)

## Tip

- 全屏 API，切换全屏时监听`fullscreenchange`事件，还需要判断文档 `fullscreenElement` 非空（`null`）时则为全屏模式，主动进入全屏方法为`document.documentElement?.requestFullscreen();`，退出全屏方法为`document?.exitFullscreen();`，H5可以监听Native返回键以退出全屏播放而不直接退出页面，在使用videojs全屏播放视频后如果DOM有修改也会触发退出全屏

```js
/* 参考 https://developer.mozilla.org/zh-CN/docs/Web/API/Fullscreen_API */

function toggleFullScreen() {
  if (!document.fullscreenElement) {
      document.documentElement.requestFullscreen();
  } else {
    if (document.exitFullscreen) {
      document.exitFullscreen();
    }
  }
}
```

- MutationObserver、IntersectionObserver 使用场景(另外还有其他观察器 PerformanceObserver 用于Web Worker性能观察、ResizeObserver 用于元素边界改变观察)
  - [Mutation observer(DOM 变动观察器)](https://developer.mozilla.org/zh-CN/docs/Web/API/MutationObserver/MutationObserver)，用于观察 DOM 元素，在其发生更改时触发回调，可用于跟踪代码其他部分引入的DOM更改如动态代码的高亮显示、删除第三方脚本生成的DOM；vue2之前有使用过MutationObserver作为Promise的降级处理方案，属于microtask，下一次渲染DOM后执行回调
  - [Intersection Observer API](https://developer.mozilla.org/zh-CN/docs/Web/API/Intersection_Observer_API)则是异步检测目标元素与祖先元素或 viewport 视口相交方法，场景有图片懒加载即图片滚动为可见时加载、无限滚动即滚动到底部时直接加载下一页、上报广告曝光、某区域可见时执行任务或播放动画，注意回调函数会在主线程中被执行若有一些耗时的操作需要执行，MDN上是建议使用 Window.requestIdleCallback() 方法
  
```js
/* 参考 Mutation observer  */
function callback(mutationList, observer) {
  mutationList.forEach((mutation) => {
    switch(mutation.type) {
      case 'childList':
        /* 从树上添加或移除一个或更多的子节点；参见 mutation.addedNodes 与
           mutation.removedNodes */
        break;
      case 'attributes':
        /* mutation.target 中某节点的一个属性值被更改；该属性名称在 mutation.attributeName 中，
           该属性之前的值为 mutation.oldValue */
        break;
    }
  });
}
var targetNode = document.querySelector("#someElement");
var observerOptions = {
  childList: true,  // 观察目标子节点的变化，是否有添加或者删除
  attributes: true, // 观察属性变动
  subtree: true     // 观察后代节点，默认为 false
}

var observer = new MutationObserver(callback);
observer.observe(targetNode, observerOptions);

var mutations = observer.takeRecords();

if (mutations) {
  callback(mutations);
}

observer.disconnect();

/* 参考 Intersection Observer API  */
/* 创建 IntersectionObserver对象，并传入相应参数和回调用函数，该回调函数将会在目标(target)元素和根(root)元素的交集大小超过阈值(threshold)规定的大小时候被执行。 */
let options = {
    // 必须是目标元素的父级元素。如果未指定或者为null，则默认为浏览器视窗
    root: document.querySelector('#scrollArea'),
    // 根(root)元素的外边距，控制根元素的收缩与扩展
    rootMargin: '0px',
    // number(可见程度0-1)或number数组类型(每到一个可见度间隔回调)，
    threshold: 0 // [0, 0.25, 0.5, 0.75, 1]
}
// 回调接收 IntersectionObserverEntry 对象和观察者的列表
let callback =(entries, observer) => {
  entries.forEach(entry => {
    // Each entry describes an intersection change for one observed
    // target element:
    //   entry.boundingClientRect
    //   entry.intersectionRatio
    //   entry.intersectionRect
    //   entry.isIntersecting
    //   entry.rootBounds
    //   entry.target
    //   entry.time
  });
};

let observer = new IntersectionObserver(callback, options);
// 为每个观察者配置一个目标
let target = document.querySelector('#listItem');
// 开始监听，同时有停止监听的方法disconnect()、unobserve()、takeRecords()
observer.observe(target);
```

## Share

[【第2208期】SPA 路由三部曲之实战演练](https://mp.weixin.qq.com/s/SJXwhTo4j6I3WMmQuOOs7A)
