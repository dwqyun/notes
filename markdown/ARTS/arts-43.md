# ARTS第四十三周

> ARTS是什么？  
  *Algorithm*：每周至少做一个LeetCode的算法题  
  *Review*：阅读并点评至少一篇英文技术文章  
  *Tip*：学习至少一个技术技巧  
  *Share*：分享一篇有观点和思考的技术文章  

## Algorithm

[单词频率](https://leetcode-cn.com/problems/words-frequency-lcci/)

```js
/* 设计一个方法，找出任意指定单词在一本书中的出现频率。

你的实现应该支持如下操作：

WordsFrequency(book)构造函数，参数为字符串数组构成的一本书
get(word)查询指定单词在书中出现的频率
示例：

WordsFrequency wordsFrequency = new WordsFrequency({"i", "have", "an", "apple", "he", "have", "a", "pen"});
wordsFrequency.get("you"); //返回0，"you"没有出现过
wordsFrequency.get("have"); //返回2，"have"出现2次
wordsFrequency.get("an"); //返回1
wordsFrequency.get("apple"); //返回1
wordsFrequency.get("pen"); //返回1
提示：

book[i]中只包含小写字母
1 <= book.length <= 100000
1 <= book[i].length <= 10
get函数的调用次数不会超过100000 */

/**
 * @param {string[]} book
 */
var WordsFrequency = function (book) {
  this.map = new Map();
  for (const word of book) {
    this.map.set(word, (this.map.get(word) || 0) + 1);
  }
};

/**
 * @param {string} word
 * @return {number}
 */
WordsFrequency.prototype.get = function (word) {
  return this.map.get(word) || 0;
};

/**
 * Your WordsFrequency object will be instantiated and called as such:
 * var obj = new WordsFrequency(book)
 * var param_1 = obj.get(word)
 */
```

## Review

[Don't trust default timeouts](https://robertovitillo.com/default-timeouts/)

## Tip

- 获取鼠标选中区域内的元素可以使用Range API 的 `getSetSelection`，结合文档片段fragment可以对节点进行DOM操作，文档片段插入到DOM中时是添加片段的子节点，只访问一次实时的DOM和触发一次重排

```js
/* 如利用 Range 和 fragment  将子节点倒序排*/
function reverseChildren(element) {
  let range = new Range();

  range.selectNodeContents(element);

// 从文档树移动Range内容到DocumentFragment（文档片段对象）
  let fragment = range.extractContents();
  let len = fragment.childNodes.length;

  while (len-- > 0) {
    fragment.appendChild(fragment.childNodes[len])
  }
  element.appendChild(fragment);
}
```

- try-catch应该使用于不确的错误如调用第三方API，如果错误可预知应该使用更合理的方式处理，如error first、if-else以及promise.reject；与with语句、eval类似try-catch的catch字句是动态作用域，引擎难以静态分析代码来优化标识符查找，所以使用try-catch的catch字句时应该尽量简化，如将错误委托给一个`handleError(e)`函数处理以减少局部变量访问，如A函数中使用try包裹return [null, await promise()]，catch中return [error, res]

```js
  const [error, data] = await api();

  if (error) {
    promise.reject(error);
  }
  
  try {
    const [error, data] = await api();
    return [error, res];
  } catch (error) {
    handleError(error);
    // return [error, undefined];
  }
```

## Share

[【第2055期】如何用JavaScript检测空闲的浏览器标签](https://mp.weixin.qq.com/s/pT9e5vtUCdnpwIBnu7vqmQ)
