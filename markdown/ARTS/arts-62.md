# ARTS第六十二周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[整数替换](https://leetcode-cn.com/problems/integer-replacement/)

```js
/*
整数替换
给定一个正整数 n ，你可以做如下操作：

如果 n 是偶数，则用 n / 2替换 n 。
如果 n 是奇数，则可以用 n + 1或n - 1替换 n 。
n 变为 1 所需的最小替换次数是多少？

示例 1：

输入：n = 8
输出：3
解释：8 -> 4 -> 2 -> 1
示例 2：

输入：n = 7
输出：4
解释：7 -> 8 -> 4 -> 2 -> 1
或 7 -> 6 -> 3 -> 2 -> 1
示例 3：

输入：n = 4
输出：2

提示：

1 <= n <= 231 - 1
*/

/**
 * @param {number} n
 * @return {number}
 */
var integerReplacement = function (n) {
  let count = 0;
  while (n !== 1) {
    if ((n & 1) === 0) {
      // 偶数右移
      n >>>= 1;
    } else {
      // 奇数判断 二进制11结尾则+1处理 3或01则-1处理
      n = (((n & 2) === 0) || n === 3) ? n - 1 : n + 1;
    }
    count++;
  }
  return count;
};
```

## Review

[10 bad TypeScript habits to break this year](https://startup-cto.net/10-bad-typescript-habits-to-break-this-year/)

## Tip

- 使用vue-cli构建项目后，运行 `vue-cli-service build` 可以添加 --target 选项构建目标，如目标值为`lib`，可将指定入口构建为[库](https://cli.vuejs.org/zh/guide/build-targets.html#%E5%BA%93)输出，CSS分离可以在vue.config.js 中设置` css: { extract: true } `，Lib打包命令还可以配置生成库js名， babel引用库中的umd.js文件若import和require混用会出现错误，可以在`.babelrc`添加`modules: "commonjs"`配置，或在引用的处添加`sourceType: unambiguous`配置；Lib项目package.json中可以设置`main: "./lib/myLib.umd.js"`和`module: "./src/index.js"`配置不同的导出方式，`module`支持esm import引用
  
```bash
<!-- 打包lib命令 -->
vue-cli-service build --target lib --formats umd --name myLib --entry src/index.js
```

```js

// 引用自: @vue\cli-service\lib\commands\build\resolveLibConfig.js
    rawConfig.output = Object.assign({
      library: libName,
      libraryExport: isVueEntry ? 'default' : undefined,
      libraryTarget: format,
      // preserve UDM header from webpack 3 until webpack provides either
      // libraryTarget: 'esm' or target: 'universal'
      // https://github.com/webpack/webpack/issues/6522
      // https://github.com/webpack/webpack/issues/6525
      globalObject: `(typeof self !== 'undefined' ? self : this)`
    }, rawConfig.output, {
      filename: `${entryName}.js`,
      chunkFilename: `${entryName}.[name].js`,
      // use dynamic publicPath so this can be deployed anywhere
      // the actual path will be determined at runtime by checking
      // document.currentScript.src.
      publicPath: ''
    })
```

## Share

[补齐v8基础知识（一）v8与JavaScript简介](https://mp.weixin.qq.com/s/XB3n7aGz6ntPRJwwaDSRMw)
