# ARTS第七十二周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

```js
/*
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。



示例 1:

输入: s = "abcabcbb"
输出: 3
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
示例 4:

输入: s = ""
输出: 0


提示：

0 <= s.length <= 5 * 104
s 由英文字母、数字、符号和空格组成
*/
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function (s) {
  const charSet = new Set();
  const len = s.length;
  // 右指针 左指针
  let rightIndex = -1, maxLen = 0;
  for (let i = 0; i < len; ++i) {
    if (i != 0) {
      // 左指针向右 移除一个字符
      charSet.delete(s.charAt(i - 1));
    }

    // 移动右指针
    while (rightIndex + 1 < len && !charSet.has(s.charAt(rightIndex + 1))) {
      charSet.add(s.charAt(rightIndex + 1));
      ++rightIndex;
    }
    // 无重复字符子串
    maxLen = Math.max(maxLen, rightIndex - i + 1);
  }
  return maxLen;
};
```

## Review

[Centering in CSS](https://web.dev/centering-in-css/)

- Content Center

  ```css
    display: grid;
    place-content: center;
    gap: 1ch;
  ```

- Gentle Flex

  ```css
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 1ch;
  ```

- Autobot

  ```css
    display: flex;
    & > * {
      margin: auto;
    }
    
    .autobot {
      display: flex;
    }
    .autobot > * {
      margin: auto;
    }

  ```

- Fluffy Center

  ```css
    padding: 15vmin;

    .fluffy-center {
      padding: 10ch;
    }

- Pop & Plop

  ```css
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
  ```

## Tip

- [Symbol 类型](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Symbol)
  - 对象的属性键只能是字符串类型或者 Symbol 类型，symbol是基本数据类型，symbol值作为对象属性的唯一标识符是主要作用
  - `Symbol(description)`函数可创建带描述的值，不支持构造函数`new`调用， Symbol 包装器对象需要使用`Object(Symbol(description))`创建
  - 全局Symbol值可以用 `Symbol.for()` 和  `Symbol.keyFor()` 方法从全局的symbol注册表设置和取得symbol
  - Symbol“隐藏” 对象属性的特定可用于创建私有属性，Symbol 属性不会出现在 for..in 、Object.keys中，不会被直接访问；Object.assign可以复制Symbol属性， `Object.getOwnPropertySymbols(obj)`和`Reflect.ownKeys(obj)`可以获取

```js
let id = Symbol.for("id");
let idAgain = Symbol.for("id");
alert( id === idAgain ); // true

let sym = Symbol.for("name");
alert( Symbol.keyFor(sym) ); // name

var sym = Symbol("foo");
var obj = {[sym]: 1};
obj[sym];            // 1
obj[Object(sym)];    // still 1
```

## Share

[一文搞懂Web常见的攻击方式](https://mp.weixin.qq.com/s/Wic__-qqkPvZKqrByuPp2g)
