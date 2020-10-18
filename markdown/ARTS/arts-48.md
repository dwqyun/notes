# ARTS第四十八周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[构建乘积数组](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)

```js
/* 构建乘积数组
给定一个数组 A[0,1,…,n-1]，请构建一个数组 B[0,1,…,n-1]，其中 B 中的元素 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。

示例:

输入: [1,2,3,4,5]
输出: [120,60,40,30,24]

提示：

所有元素乘积之和不会溢出 32 位整数
a.length <= 100000 */
/**
 * @param {number[]} a
 * @return {number[]}
 */
var constructArr = function (a) {
  const len = a.length;
  if (len === 0) {
    return [];
  }

  const res = new Array(len);
  let temp = 1;
  res[0] = 1;
  /* a[0] * res[0] = a[i] * res[i] 分上下三角计算
    res[0]  1     a[1]  a[2]  ...  a[n-1] a[n]
    res[1]  a[0]  1     a[2]  ...  a[n-1] a[n]
    res[2]  a[0]  a[1]  1     ...  a[n-1] a[n]
    ...
  res[n-1]  a[0]  a[1]  1     ...  1      a[n]  
    res[n]  a[0]  a[1]  1     ...  a[n-1] 1
   */
  for (let i = 1; i < len; i++) {
    res[i] = res[i - 1] * a[i - 1];
  }
  // 计算上三角 得res[i]值为a的数组除i外索引的值乘积
  for (let i = len - 2; i >= 0; i--) {
    temp *= a[i + 1];
    res[i] *= temp;
  }
  return res;
};
```

## Review

[My Favorite JavaScript Tips and Tricks](https://blog.greenroots.info/my-favorite-javascript-tips-and-tricks-ckd60i4cq011em8s16uobcelc)

## Tip

- vue的v-model指令常用于表单控件和自定义组件，支持`.lazy`、`.number`、`.trim`修饰符，v-model负责监听表单控件输入事件(input、change)以更新数据(value、check)，一个自定义组件上的 v-model 默认会利用名为 value 的 prop 和名为 input 的事件，也可以通过`model`重新定义需要通过事件更新的props值，如弹框自定义组件使用model配合emit事件更新传入的props绑定值

```html
<dialog-component v-model="propsKey"></dialog-component>
```

```js
Vue.component('base-checkbox', {
  model: {
    prop: 'visible',
    event: 'visible-change'
  },
  props: {
    visible: Boolean
  },
  methods: {
    close() {
      this.$emit('visible-change', false);
    }
  },
  template: `
    <div role="dialog" v-show="visible">
      <div class="body">
        <button @click=close></button>
      </div>
    </div>
  `
})

/* vue源码 */
// transform component v-model info (value and callback) into
// prop and event handler respectively.
function transformModel (options, data) {
  var prop = (options.model && options.model.prop) || 'value';
  var event = (options.model && options.model.event) || 'input'
  ;(data.attrs || (data.attrs = {}))[prop] = data.model.value;
  var on = data.on || (data.on = {});
  var existing = on[event];
  var callback = data.model.callback;
  if (isDef(existing)) {
    if (
      Array.isArray(existing)
        ? existing.indexOf(callback) === -1
        : existing !== callback
    ) {
      on[event] = [callback].concat(existing);
    }
  } else {
    on[event] = callback;
  }
}
```

## Share

[flex:0 flex:1 flex:none flex:auto应该在什么场景下使用？](https://www.zhangxinxu.com/wordpress/2020/10/css-flex-0-1-none/)
