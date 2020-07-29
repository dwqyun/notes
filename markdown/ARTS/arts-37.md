# ARTS第三十七周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[幂集](https://leetcode-cn.com/problems/power-set-lcci)

```js
/* 编写一种方法，返回某集合的所有子集。集合中不包含重复的元素。

说明：解集不能包含重复的子集。

示例:

 输入： nums = [1,2,3]
 输出：
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
] */
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsets = function (nums) {
  const setArr = [...new Set(nums)];
  const res = [[]];

  while (setArr.length) {
    const curNum = setArr.pop();
    const arr = [[curNum]];

    for (const i in setArr) {
      const map = arr.map(item => [...item, setArr[i]])
      arr.push(...map);
    }
    res.push(...arr);
  }
  return res;
};
```

## Review

[20 Essential JavaScript Interview Questions]<https://kentcdodds.com/blog/javascript-default-parameters>)

## Tip

- 使用`cross-fade()`实现背景图片透明效果，如两张图片透明混合`background-image: cross-fade(url(img1.png), url(img2.png), 50%);`
- 函数缓存功能可以入参一致时返回缓存结果

  ```js
      function memoize(func) {
        let cache = {};

        function inner(...args) {
            const key = JSON.stringify(args);

            if(key in cache)
                return cache[key];

            cache[key] = func.apply(this, args);

            return cache[key];
        }

        return inner;
    }
  
  ```

## Share

[揭秘webpack插件的工作原理](https://mp.weixin.qq.com/s/AWIJeh0uTxgH2XG6mSaY5g)
