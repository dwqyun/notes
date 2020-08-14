# ARTS第四十周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[求1+2+…+n](https://leetcode-cn.com/problems/qiu-12n-lcof/)

```js
/*
求 1+2+...+n ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。


示例 1：

输入: n = 3
输出: 6
示例 2：

输入: n = 9
输出: 45


限制：

1 <= n <= 10000 */
/**
 * @param {number} n
 * @return {number}
 */
var sumNums = function (n) {
  // 等差数列求和公式 1 + 2 + ... + n = n(n + 1) / 2
  return (Math.pow(n, 2) + n) >> 1;
};
```

## Review

[ES6 Template Literals in Depth](https://ponyfoo.com/articles/es6-template-strings-in-depth)

## Tip

- 在使用`router.push`重进相同路由时会报错，V3.1.0版本中push和replace方法会返回的是promise可以主动catch，可以对VueRouter.prototype上的push、replace方法进行重写，统一处理异常，如根据错误类型进行Toast提示，Vue Router中`router.app`代表了配置了 router 的 Vue 根实例，可以使用app属性访问Vue原型上的Toast方法或者进行$store更新
  
> [参考vue-router-issue](https://github.com/vuejs/vue-router/issues/2881)

```js
import Router from 'vue-router'

const originalPush = Router.prototype.push
Router.prototype.push = function push(location, onResolve, onReject) {
  if (onResolve || onReject) {
    return originalPush.call(this, location, onResolve, onReject)
  };
  return originalPush.call(this, location).catch(err => {
    // Vue根实例
    const vm = this.app;

    // 重复进入错误处理
    if (err instanceof === NavigationDuplicated) {
      // xxx
    }
    vm.$store.dispatch('xxx');
    vm.$toast('xxx');
    vm.$log(err);
  });
}

```

- 使用Vue keep-alive时可以配合Router scrollBehavior方法自定义路由切换时页面如何滚动，如果是页面是区域内滚动元素则可以使用钩子函数`deactivated`记录切换前元素滚动位置，`activated`则处理回滚操作，若页面是动态keep-alive则可以使用Vuex更新keep-alive的`include`组件名字符串数组

## Share

[【第2028期】What I'm thinking about: JS疲劳、招聘](https://mp.weixin.qq.com/s/42r-HqT8UOvQV-mLgkYHpA)
