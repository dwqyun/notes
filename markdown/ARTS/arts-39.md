# ARTS第三十九周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[交换和](https://leetcode-cn.com/problems/sum-swap-lcci)

```js
/* 给定两个整数数组，请交换一对数值（每个数组中取一个数值），使得两个数组所有元素的和相等。

返回一个数组，第一个元素是第一个数组中要交换的元素，第二个元素是第二个数组中要交换的元素。若有多个答案，返回任意一个均可。若无满足条件的数值，返回空数组。

示例:

输入: array1 = [4, 1, 2, 1, 1, 2], array2 = [3, 6, 3, 3]
输出: [1, 3]
示例:

输入: array1 = [1, 2, 3], array2 = [4, 5, 6]
输出: []
提示：

1 <= array1.length, array2.length <= 100000*/

/**
 * @param {number[]} array1
 * @param {number[]} array2
 * @return {number[]}
 */
var findSwapValues = function (array1, array2) {
  // 数组值总和
  const sum1 = array1.reduce((val, sum) => val + sum);
  const sum2 = array2.reduce((val, sum) => val + sum);
  const diff = sum1 - sum2;
  // 两数总和差为偶数 sum1 - sum2 = 2(val1 -val2)
  if (diff & 1) {
    return [];
  }

  // 使用Set集合去重循环
  const set1 = new Set(array1);
  for (const val1 of set1) {
    // 求交换值是否在另一数组
    const val2 = val1 - diff / 2;
    if (array2.includes(val2)) {
      return [val1, val2];
    }
  }

  return [];
};
```

## Review

[ES6 Proxies in Depth](https://ponyfoo.com/articles/es6-proxies-in-depth)

## Tip

- 如果项目依赖有需要额外转译ES语法的，需要排除指定模块名，在`babel-loader`使用`exclude`或`include`都可以，只需要注意options里的每一项配置都是数组；如果是使用`vue-cli`则配置`transpileDependencies`显式转译一个依赖

```js
/* webpack.config.js */

rules: [
  {
    test: /\.m?js$/,
    // exclude: /node_modules\/(?!myModule\/).*/,
    include: [path.join(__dirname, 'src'), path.join(__dirname, 'node_modules/myModule')],
    use: {
      loader: 'babel-loader',
      options: {
        presets: [
          [
            "@babel/preset-env",
            {
              useBuiltIns: "entry"
            }
          ]
        ],
        plugins: ['@babel/plugin-transform-runtime']
      }
    }
  }
]

/* vue.config.js */

transpileDependencies: ['/node_modules/myModule/']
```

## Share

[【第2022期】不定宽溢出文本适配滚动](https://mp.weixin.qq.com/s/rtdMStqBhe0sV-wC6Q98gQ)
