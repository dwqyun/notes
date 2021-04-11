# ARTS第六十六周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

```js
/* 
剑指 Offer 04. 二维数组中的查找 
在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

示例:

现有矩阵 matrix 如下：
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。

给定 target = 20，返回 false。

限制：

0 <= n <= 1000

0 <= m <= 1000
*/
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var findNumberIn2DArray = function (matrix, target) {
  // 以数组左下角为原点 若当前数小于目标数则右移 若大于目标则上移一位
  const n = matrix.length;
  if (!n) {
    return false;
  }
  const m = matrix[0].length;
  let x = n - 1;
  let y = 0;
  while (x >= 0 && y < m) {
    if (matrix[x][y] === target) {
      return true;
    }
    matrix[x][y] > target ? x-- : y++;
  }
  return false;
};
```

## Review

[How to Apply CSS3 Transforms to Background Images](https://www.sitepoint.com/css3-transform-background-image/)

## Tip

- [Vue Router](https://router.vuejs.org/zh/api/#router-link) 使用小结
  - `this.$route`(路由信息对象)，属性是只读的，当路由导航变化时可watch (监测变化) 它，`this.$route.query.from=xxx`可修改属性值但不会触发`watch`且地址URL不会即时更新，可使用编程导航修改URL参数`router.push({ query: { from: 'xxx' }})`，this.$route对象引用会变动触发watch
  - 使用router.replace只剩余一个导航历史时，调用router.back无效需要注意判断history长度；`router.replace`和`router.push`返回的是promise，支持`router.pus(location, onComplete?, onAbort?)`或`router.push(location).then(onComplete).catch(onAbort)`，可对`VueRouter.prototype`上的push、replace方法进行重写，便于统一处理导航异常，如根据错误类型进行Toast提示，
  - Vue Router中`router.app`代表了配置了 router 的 Vue 根实例，可以使用app属性访问Vue原型上的方法属性，或调用$store更新网络状态
  - `router.onReady(callback, [errorCallback])`在路由完成初始导航时回调，可以解析异步进入钩子和路由初始化相关联的异步组件，组件mounted时router也可能尚未初始化完成，onReady回调阶段可获取query上的参数可用于请求接口依赖URL参数场景
  - `router.onError(callback)`回调会在路由导航过程中出错时被调用，可在APP.vue统一注册导航错误处理事件，如懒加载使用异步组件时，网络中断无法跳转下一个路由可在onError中判断网络状态再提升用户，此外可使用`isNavigationFailure`检测导航故障
  
> 参考 [导航故障](https://router.vuejs.org/zh/guide/advanced/navigation-failures.html#%E6%A3%80%E6%B5%8B%E5%AF%BC%E8%88%AA%E6%95%85%E9%9A%9C)

```js
/* APP */
created () {
  this.$router.onReady(() => {
    const { xxx } = this.$route.quey;
    this.$axios.post('url', data: { xxx });
  })
  this.$router.onError(async() => {
    await checkNetworkStatus();
    if (!this.isNetworkAccessible) {
      this.$toast('网络断开，请检查网络')
    }
  })
},

/* router */
import Router from 'vue-router'
const { isNavigationFailure, NavigationFailureType } = VueRouter

const originalPush = Router.prototype.push
Router.prototype.push = function push(location, onResolve, onReject) {
  if (onResolve || onReject) {
    return originalPush.call(this, location, onResolve, onReject)
  };
  return originalPush.call(this, location).catch(err => {
    // Vue根实例
    const vm = this.app;

    // 重复进入错误处理 或 检查 isNavigationFailure NavigationFailureType
    if (err instanceof === NavigationDuplicated) {
      // xxx
    }
    vm.$store.dispatch('xxx');
    vm.$toast('xxx');
  });
}

// 正在尝试访问 admin 页面
/* 如果你忽略第二个参数：isNavigationFailure(failure)，那么就只会检查这个错误是不是一个导航故障；有四种不同的类型值
redirected：在导航守卫中调用了 next(newLocation) 重定向到了其他地方。
aborted：在导航守卫中调用了 next(false) 中断了本次导航。
cancelled：在当前导航还没有完成之前又有了一个新的导航。比如，在等待导航守卫的过程中又调用了 router.push。
duplicated：导航被阻止，因为我们已经在目标位置了
 */
router.push('/admin').catch(failure => {
  if (isNavigationFailure(failure, NavigationFailureType.redirected)) {
    // 向用户显示一个小通知
    showToast('Login in order to access the admin panel')
  }
})
```

## Share

[【第2247期】99% 开发者没弄明白的 babel 知识](https://mp.weixin.qq.com/s/sJMydobsSxzxj2SECwcr_A)
