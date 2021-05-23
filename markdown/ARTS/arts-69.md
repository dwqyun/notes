# ARTS第六十九周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[子集](https://leetcode-cn.com/problems/subsets/)

```js
/* 
给你一个整数数组 nums ，数组中的元素 互不相同 。返回该数组所有可能的子集（幂集）。

解集 不能 包含重复的子集。你可以按 任意顺序 返回解集。

示例 1：

输入：nums = [1,2,3]
输出：[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
示例 2：

输入：nums = [0]
输出：[[],[0]]
 
提示：

1 <= nums.length <= 10
-10 <= nums[i] <= 10
nums 中的所有元素 互不相同
*/

/**
 * @param {number[]} nums
 * @return {number[][]}
 */
 var subsets = function(nums) {
    const res = [];
    const len = nums.length;
    const temp = [];
    const dfs = (index) => {
      if (index === len) {
        // 完成遍历 合并解集
        res.push([...temp]);
        return;
      }
      // 现在nums[index]后继续递归下一数
      temp.push(nums[index]);
      dfs(index + 1);
      // 上一递归结束撤销并往下递归
      temp.pop(temp.length - 1);
      dfs(index + 1);
    }
    dfs(0);
    return res;
};
```

## Review

[The lazy-loading property pattern in JavaScript](https://humanwhocodes.com/blog/2021/04/lazy-loading-property-pattern-javascript/)

- JavaScript 中的懒惰加载属性模式：通过定义对象的访问器属性`getter`方法，在访问数据属性时才生成属性值，并重新定义属性标志writable、configurable冻结属性，以实现JS对象属性懒加载访问和访问后缓存结果

```js
class MyClass {
    constructor() {

        Object.defineProperty(this, "data", {
            get() {
                const actualData = someExpensiveComputation();

                Object.defineProperty(this, "data", {
                    value: actualData,
                    writable: false,
                    configurable: false
                });

                return actualData;
            },
            configurable: true,
            enumerable: true
        });

    }
}
const object = new MyClass();
console.log(object.hasOwnProperty("data"));     // true
const data = object.data;
console.log(object.hasOwnProperty("data"));     // true

const object = {
    get data() {
        const actualData = someExpensiveComputation();

        Object.defineProperty(this, "data", {
            value: actualData,
            writable: false,
            configurable: false,
            enumerable: false
        });

        return actualData;
    }
};

console.log(object.hasOwnProperty("data"));     // true
const data = object.data;
console.log(object.hasOwnProperty("data"));     // true
```

## Tip

- 修改输入框value值触发change事件可以通过Proxy代理`HTMLInputElement.prototype.value`的setter方法，保留执行原有set方法`Object.getOwnPropertyDescriptor(HTMLInputElement.prototype, 'value').set`，结合触发自定义事件`input.dispatchEvent(new CustomEvent('change'));`实现

- 使用[CSS revert](https://developer.mozilla.org/en-US/docs/Web/CSS/revert)还原display内置值，如列表默认展示三项点击展开更多显示剩余列表，`<li>`元素display默认`list-item`才有项目符号，若使用`block`则不能显示符号可使用`revert`关键字替代

> 参考 <https://www.zhangxinxu.com/wordpress/2021/05/css-revert-display/>

```css
li:nth-child(n+4) {
    display: none;
}
```

```html
<ul id="ul">
  <li>选项1</li>
  <li>选项2</li>
  <li>选项3</li>
  <li>选项4</li>
  <li>选项5</li>
</ul>
<p><button id="b1">更多</button></p>
```

```js
li.style.display = 'block';
li.style.display = 'revert';
```

## Share

[移动端1px问题解决方案](https://mp.weixin.qq.com/s/aTp9BVfY_54KjgpV9orIGQ)
