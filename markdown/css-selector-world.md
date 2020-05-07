# 《CSS 选择器世界》读书笔记
## 1. 概述
- CSS选择器简单却很强，特定的选择符号组合成样式后，可以为用户体验提供助力。
- CSS选择器分4类，即选择器、选择符、伪类和伪元素
  - 选择器：常见的有类选择器、标签选择器、ID选择器、通配选择器...
  - 选择符：` `空格表后代、`>`表子代、`+`表直接相邻节点、`~`表兄弟节点、`||-`表列关系
  - 伪类：如:hover，有一个冒号与浏览器行为、用户行为关联
  - 伪元素: 如::before有两个冒号，会在HTML中生成相应虚拟节点
---
## 2. CSS选择器的优先级
- CSS优先级规则等级划分
  - 0级(数值0)：通配选择器(`*`)、选择符和逻辑伪类(`:not()`、`:is()`、 `:where()`)，其中只有`:is()`伪类括号中的选择器可以影响优先级
  - 1级(数值1)：标签选择器
  - 2级(数值10)：类选择器、属性选择器和伪类
  - 3级(数值100)：ID选择器，最小限度关联样式使用，为了方便重置样式优先使用类选择器
  - 4级(数值1000)：元素的style属性内联，另外`<style>`标签HTML内联样式规则优先于`<link>`标签引入的外部样式
  - 5级(数值infinite)：`!important`，顶级优先级，限制使用，可以使用的场景是使JavaScript设置无效
- `后来居上`原则
  - 优先级数值一致时后声明的优先
  - 低耦合增加优先级数值的技巧，类选择器+必然存在的属性选择器，如`.foo[class] {}`
---
## 3. CSS选择器的命名
### 选择器是否区分大小写
- 和HTML标签、属性一致，CSS的标签选择器、属性选择器对大小写不敏感
- 浏览器直接在`]`前加`i`以忽略大小写，如`[class~="val" i]`
### 选择器的命名合法性
- 首字符支持`a-z、A-Z、下划线(_)及非ASCII字符(中文、全角字符)`
- 后续字符比首字符多支持`0-9和短横线(-)`
- 选择器命名不能可以数字开头，但可以使用`Unicode`编码后的数字表示
### 选择器的命名
- CSS选择器的语义是为了方便人的识别，对于机器而言HTML的语义才显的重要，过长的单词书写和文件大小是个小负担，长命名价值有限，所以使用短命名
- 单命名可能会出现冲突，可以使用BEM(`type-block__element_modifier`，中划线作连字符，双下划线连接块与块的子元素，单下划线描述块或子元素的状态)形式的组合命名
- 面向语义是指根据元素上下文命名，面向属性是指单纯实现某一类CSS效果无关HTML结构，面向属性命名重用性高、方便快捷但场景有限，面向语义命名灵活丰富、场景宽泛但效率低，实际大项目中需要组合两种方式使用。
- 命名可以中文对应英文`专有名词`、`HTML标签`、`HTML特定属性值`、`HTML布尔属性值`、`CSS伪类`、`SVG`等参考语义化的短命名
### 选择器的最佳实践
- `不使用ID选择器`，ID选择器性能虽好但优先级太高不易覆盖，可以使用ID属性选择器替代，元素ID主要用在JS中会与JS耦合，与样式关联后可维护性大打折扣
- `不要嵌套选择器`，平常使用scss、less很容易书写出多层嵌套的样式需要更多的计算，会导致渲染性能糟糕，`CSS选择器是从右往左匹配渲染的`，使用标签选择器匹配页面元素多时也会导致渲染性能问题；过多嵌套会使优先级混乱，不能低成本重置样式；多层嵌套还会使样式布局脆弱，他限定了HTML结构，增大了维护成本；应该使用无嵌套的纯类名选择器，易扩展、易维护、代码少、性能高
- `不要歧视面向属性的命名`，场景有清除浮动、文字过长截断、公共UI样式等，可以直接在HTML class属性中加上直接使用
- `正确的使用状态类名`，页面交互上的选中、激活等状态，使用`.active`、`.checked`等(命名参考HTML属性)作为纯状态标识，即`.active`自身不带CSS样式，应该组合其他类名生成样式达到交互效果，JS中只需添加纯状态类名，使样式和行为分离，最佳实践是根据当前情况权衡出最好的实践
---
## 4. 精通CSS选择符
### 后代选择符空格
- CSS中后代选择器优先级遵循选择器优先级数值权重和后来居上原则，后代选择符会匹配所有子元素
- JS中后代选择符，`document.querySelectorAll()`为全局特性，可以使用`:scope`限制作用域，如`document.querySelector('#myId').querySelectorAll(':scope div div').length;`
### 子选择符箭头(>)
- 子选择符只匹配直接子代元素，匹配性能优于后代选择符但性能优势有限，且选用子选择符有维护成本，元素层级被绑定后续若修改层级需要调整CSS代码
- 使用子选择符主要是为了避免冲突，适用于状态类名祖先后代控制、标签重复嵌套受限、层级位置与动态判断，子选择符可以精确控制CSS影响的结构，但同时失去弹性和变化
### 相邻兄弟选择符加号(+)
- 只匹配后面相邻的一个兄弟节点
- 忽略文本节点和注释节点
- 可实现类似`:first-child`的效果，如`.cs-li + .cs-li { margin-top: 1em; }`，由于相邻兄弟选择器只匹配后一个元素，第一个不会被匹配到
- 众多高级选择器技术的核心，可以配合诸多伪类低成本实现实用的交互效果，如输入框focus时显示之前隐藏的文本提示
### 随后兄弟选择符(~)
- 与相邻兄弟选择符大体类似，区别在于随后兄弟选择符会匹配后面所有的兄弟元素
- 浏览器解析HTML文档由上而下，若CSS支持前面兄弟选择符或父选择器，则页面需要等所有子元素加载完毕才可以渲染，会造成不好的呈现体验
- 视觉上实现前面兄弟选择器效果，HTML结构不变，可以使用float、absolute、transform等具有定位特性的CSS属性，还可以使用direction、writing-mode及flex布局控制文档流呈现位置，如评星组件中的单选框可以使用`flex-flow: row-reverse;`配合`~`实现结构和视觉相反的评星效果
### 双管道选择符(||)
- 浏览器兼容性还不足以实际应用，场景是用于table和grid布局中一整列样式的控制
## 5. 元素选择器
### 选择器的级联语法
- 元素选择器包括标签选择器和通配符选择器，元素选择器是唯一不能重复自身的选择器，且元素选择器级联使用时必须写在最前面，如`input[type="radio"]`
- 类、ID和属性选择器都可以重复自身，且由于CSS选择器是由右往左解析，类名写在后面更好，如`[type="radio"].input`
### 标签选择器
- 标签选择器一般使用与固定组合的标签元素，如原生的表格、列表
- 如果原生属性是某些标签元素特有的，那么标签选择器可以忽略，直接使用书写选择器
- IE9以上支持自定义元素标签选择器
### 通配符选择器
- 指代所有类型的标签元素，包括自定义元素和`<script>`、`<style>`、`<title>`等，但不含伪元素，重置样式可`*, ::before, ::after {}`，通配符和其他选择器级联使用时可以省略星号，只有单独使用通配符时才呈现星号字符
---
## 6. 属性选择器
### ID选择器和类选择器
- 同属属性选择器，但语法、优先级以及可重复性不同
### 属性值直接匹配选择器
- `[attr]`表示匹配包含指定的属性元素，适用于HTML布尔属性如disabled，但有一个特例是`[checked]`选择器，表单控件在checked状态变化时并不会同步修改checked属性的值，需要JS赋值DOM属性checked修复或者使用`:checked`伪类替代`[checked]`
- [attr="val"]是属性值完全匹配选择器，如`[data-type="1"]`，若属性值包含空格则需要转义
- [attr~="val"]是属性值单词完全匹配选择器，用于匹配关键词
- [attr!="val"]是属性值起始平淡完全匹配选择器，表示元素属性其值正好是val或val-(U+002D)开头
- AMCSS(Attribute Modules for CSS)表示借助HTML属性进行CSS开发
### 属性值正则匹配选择器
- [attr^="val"]表匹配attr熟悉值已字符val开头的元素，可以匹配中文，一般用于匹配a元素的链接地址类型
- [attr$="val"]表匹配attr属性值以字符val结尾的元素，一般用于判断链接后缀
- [attr*="val"]表匹配attr属性值包含字符val的元素，如匹配style属性值`[style*="none"]`
- 字母i忽略属性值大小写正则匹配运算符，如`[data-search]:not([data-search*="value" i]) { display: none }`
---
## 7. 用户行为伪类
### 手型经过伪类:hover
- :hover用于移动端虽然可以触发但消失不敏捷，常用于桌面端网页，实现按钮颜色变化、tips提升或下拉等效果
- :hover延时体验优化，使用后代或兄弟节点+`visibility`属性+CSS `transition`设置延迟显示,transition对display无过度效果
- 需要注意带交互效果的的行为，还要辅以其他手段优化体验，如结合:focus伪类优化用户不能:hover时的体验
### 激活状态伪类:active
- 点按触发元素激活时的样式，支持任意HTML元素包括自定义元素，键盘访问无法触发，主要用于反馈点击使得交互，不适用于复杂的交互
- 移动端图片可以使用`outline`+`clip-path`实现通用的:active反馈效果，body适用`-webkit-tap-highlight-color`，按钮链接类使用 `linear-gradient`
- 使用:active+伪元素给按钮埋点，如`.button-1:active::after {content: url(./pixel.gif?action=click&id=button1); display: none;}`
### 焦点伪类:focus
- 只匹配特定的元素，非disabled状态的表单元素(如input、select、button)、包含href属性的a元素、area元素、summary元素，普通元素需要设置`contenteditable``或tabindex`属性，一个页面只会有一个焦点元素只有这个元素响应:focus样式
- 浏览器已经优化了点击链接显示轮廓的体验，`* ｛ outline: 0 none; ｝`这类无差别重置outline的写法没必要且会影响使用键盘进行无障碍访问，focus时通过虚框发光仪标记用户目前访问的元素是很有必要的
- :focus伪类与无障碍访问密切相关，span、div元素可以模拟按钮UI效果，但不支持button的原生属性需要额外加tab键索引或`role=button`，可以使用label元素模拟按钮效果，方便保留语义和原生行为，如input和label关联嵌套，可以使用`position: absolute; clip: rect(0 0 0 0);`隐藏input标签，或`opacity: 0`隐藏，`visibility: hidden`和`display: none`的隐藏会导致键盘无法聚焦
### 整体焦点伪类:focus-within
- 与:focus伪类不同的是，:focus-within伪类样式在当前元素或当前元素的任意子元素处于聚焦状态时都会匹配，子元素聚焦可以使父级元素样式发生变化，属于“父选择器”行为，但需要用户行为触发属于后渲染，不与现有的渲染机制相冲突
- :focus-within可实现无障碍访问的下拉列表交互，聚焦子元素时都会触发父元素设置的:focus-within伪类样式使下拉列表保持显示状态
### 键盘焦点伪类:focus-visible
- :focus-visible伪类匹配场景是，元素聚焦且浏览器认为聚焦轮廓应该显示，可以解决Chrome下鼠标点击访问时的轮廓显示问题，浏览器认为使用键盘访问触发的元素聚焦才是:focus-visible表示的聚焦，`:focus:not(:focus-visible) { outline: 0; }`即可以去除Chrome下鼠标点击时的outline而暴力流键盘访问时的outline
---
## 8. URL定位伪类
### 链接历史伪类:link和:visited
- :link伪类匹配页面上href链接没有访问过的a元素，a、link、area都支持盒饭属性，但:link伪类只能匹配a元素；:visited匹配访问过的a元素，一般使用a标签选择器设置默认链接颜色，有其他需求才使用伪类；a标签选择器会匹配无href属性a元素，但:link只会匹配有href属性的a元素，实际使用中可以使用`[href]`属性选择器替代a标签选择器
- :visited伪类只支持color相关的CSS属性且不支持::before和:after这些伪元素；使用:visited控制颜色表现只支持纯色或透明；且只能重置默认已有的颜色，不能凭空设置颜色；使用getComputedStyle无法获取:visited设置的颜色值
###  超链接伪类:any-link
- 相对:link伪类和a标签选择器效果无差别且a标签设置更简单的情况，`:any-link`可以匹配所有href属性的链接元素，且匹配:link或:visited伪类的元素，也可以精确识别href属性元素，是真正意义上的链接伪类
### 目标伪类:target
- URL瞄点即hash值可以和页面中id匹配的元素进行瞄定，浏览器默认行为是触发滚动定位，同时进行:target伪类匹配，如果瞄点元素是display:none则浏览器不会触发任何滚动但可以匹配:target伪类样式
- :target的交互布局技术，结合a标签和兄弟选择器实现展开收起效果(可以通过URL记住当前页面交互状态)、结合隐藏的瞄链元素、兄弟选择及JS类名绑定实现选项卡tab效果
### 目标容器伪类:target-within
- :target-within可以匹配:target伪类匹配的元素，或者匹配存在后代元素(包括文本节点)匹配:target伪类的元素，含义与:focus-within类似但浏览器尚未支持兼容性欠佳
---
## 9. 输入伪类
### 输入控件状态
- 可用状态与禁用状态伪类:enabled和:disabled，两者对立，:enabled在CSS开发中有些鸡肋，表单元素默认就是enabled状态，不需要额外的:enabled伪类匹配；在JS中可以使用`document.querySelectorAll('form:enabled')`查询所有可用表单元素，以实现自定义表单序列化方法，:disabled常用于按钮，设置按钮DOM属性disabled=true即可，对于a元素常使用`pointer-events:none`控制点击无效，但tab键盘仍然可以访问且回车键也可以触发点击事件，属于伪禁用，同时元素的title无法显示，可用性降低，所以尽量使用原生按钮实现交互效果
- 读写特性伪类:read-only和:read-write，用于匹配是否可读和是否可读可写，只作用于input和textarea元素，由于输入框默认状态就是:read-write所以很少使用，一般使用:read-only对处于readonly状态的输入框进行样式重置，readonly和disabled区别在于，readonly可以被表单提交，而disabled不能被表单提交且文字会被置灰
- 占位显示伪类:placeholder-shown，当输入框的placeholder内容显示时匹配该输入框，而placeholder只在输入框空值状态才显示，即可以根据:placeholder-shown伪类判断输入框是否有值可用于必填内容验证提示交互，也可用于纯CSS实现Material Design风格占位文本交互效果，主要使用绝对定位的label根据是否聚焦和placeholder是否可见来进行label的变形效果，代码如下
```html
<div class="input-fill-x">
  <input class="input-fill" placeholder="邮箱">
  <label class="input-label">邮箱</label>
```
```css
.input-fill-x {
  position: relative;
}
.input-label {
  position: absolute;
  left: 16px;
  top: 14px;
  pointer-events: none;
}
.input-fill:not(:placeholder-shown) ~ .input-label,
.input-fill:focus ~ .input-label {
  transform: scale(0.75) translate(0, -32px);
}
- 默认选项伪类:default，只作用域处于默认状态的表单元素，如select元素下的默认option，凸显用户选择一组数据时仍可知道默认选项是什么，增强了用户体验；:default虽然是用于标记默认状态避免混淆，但更重要的实际价值可以用于`推荐标记`，如支付方式中默认选中微信，选项为"微信(推荐)"，可以使用:default伪类使默认状态为checked的选项自动加推荐标记，方便维护，如`input:default + label::after { content: ' (推荐) ' }`
### 输入值状态
```
### 
---
## 10. 树结构伪类
---
## 11. 逻辑组合伪类
---
## 12. 其他伪类选择器
