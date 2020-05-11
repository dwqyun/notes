# 《CSS 选择器世界》读书笔记

## 1. 概述

- CSS选择器简单却很强，特定的选择符号组合成样式后，可以为用户体验提供助力。
- CSS选择器分4类，即选择器、选择符、伪类和伪元素
  - 选择器：常见的有类选择器、标签选择器、ID选择器、通配选择器...
  - 选择符：``空格表后代、`>`表子代、`+`表直接相邻节点、`~`表兄弟节点、`||-`表列关系
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

- 与:focus伪类不同的是，`:focus-within`伪类样式在当前元素或当前元素的任意子元素处于聚焦状态时都会匹配，子元素聚焦可以使父级元素样式发生变化，属于“父选择器”行为，但需要用户行为触发属于后渲染，不与现有的渲染机制相冲突
- :focus-within可实现无障碍访问的下拉列表交互，聚焦子元素时都会触发父元素设置的:focus-within伪类样式使下拉列表保持显示状态

### 键盘焦点伪类:focus-visible

- :focus-visible伪类匹配场景是，元素聚焦且浏览器认为聚焦轮廓应该显示，可以解决Chrome下鼠标点击访问时的轮廓显示问题，浏览器认为使用键盘访问触发的元素聚焦才是:focus-visible表示的聚焦，`:focus:not(:focus-visible) { outline: 0; }`即可以去除Chrome下鼠标点击时的outline而保留键盘访问时的outline

---

## 8. URL定位伪类

### 链接历史伪类:link和:visited

- :link伪类匹配页面上href链接没有访问过的a元素，a、link、area都支持盒饭属性，但:link伪类只能匹配a元素；:visited匹配访问过的a元素，一般使用a标签选择器设置默认链接颜色，有其他需求才使用伪类；a标签选择器会匹配无href属性a元素，但:link只会匹配有href属性的a元素，实际使用中可以使用`[href]`属性选择器替代a标签选择器
- :visited伪类只支持color相关的CSS属性且不支持::before和:after这些伪元素；使用:visited控制颜色表现只支持纯色或透明；且只能重置默认已有的颜色，不能凭空设置颜色；使用getComputedStyle无法获取:visited设置的颜色值

### 超链接伪类:any-link

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
- 占位显示伪类`:placeholder-shown`，当输入框的placeholder内容显示时匹配该输入框，而placeholder只在输入框空值状态才显示，即可以根据:placeholder-shown伪类判断输入框是否有值可用于必填内容验证提示交互，也可用于纯CSS实现Material Design风格占位文本交互效果，主要使用绝对定位的label根据是否聚焦和placeholder是否可见来进行label的变形效果，代码如下

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
```

- 默认选项伪类:default，只作用域处于默认状态的表单元素，如select元素下的默认option，凸显用户选择一组数据时仍可知道默认选项是什么，增强了用户体验；:default虽然是用于标记默认状态避免混淆，但更重要的实际价值可以用于`推荐标记`，如支付方式中默认选中微信，选项为"微信(推荐)"，可以使用:default伪类使默认状态为checked的选项自动加推荐标记，方便维护，如`input:default + label::after { content: ' (推荐) ' }`

### 输入值状态

- 选中选项伪类:checked，匹配结果与[checked]属性选择器一样，但:checked只能匹配标准的表单控件元素，而[checked]属性选择器可以与任意元素匹配；`[checked]属性变化并非实时`的，所以不建议使用[checked]属性选择器控制表单复选框选中状态样式；伪类可以正确匹配从祖先元素继承的状态，而属性选择器不行如`<fieldset disabled><input></fieldset>`中fieldset设置disabled，内部元素input也会处于禁用状态，:disabled伪类可以匹配，[disabled]属性选择器不行
- 单复选框元素显隐技术，可以使用:checked伪类结合多label元素及兄弟选择器实现自定义单复选框、开关效果，祖先元素相对定位包裹绝对定位的input元素和label模拟元素，input使用opacity或clip隐藏；还可以实现标签/列表/素材的选择效果，可加以`计数器和伪类标记`选中元素
- 不确定值伪类:indeterminate，复选框处选中和非选中外，还有半选状态，多用于包含全选功能列表中，半选状态只能通过JS设置`checkbox.indeterminate = true;`，可以匹配复选框、单选框以及进度条元素progress；复选框是部分选中时匹配。单选框时多个name属性值一致但都没有选中时匹配，而进度条是未设置值时则匹配:indeterminate

### 输入值验证

- 有效验证伪类:valid:invalid，这两个伪类会在页面加载时就会匹配表单元素，新出的:user-invalid伪类则是需要用户交互后才触发但未成熟，可以在用户提交表单时通过给表单添加特定类名触发验证效果，form元素原生方法checkVaildity可以返回整个表单是否验证通过的布尔值
- 范围验证伪类:in-range和:out-of-range，常用于匹配number或range类型的输入框，可以结合:invalid伪类细化输入框出错时的提升信息
- 可选性伪类:required和:optional，设置了required和属性的表单表示必填，会匹配:required伪类，:optional伪类则与:required对立，可用于实现问卷调查的必选和可选效果，项使用ol和li元素嵌套，li元素使用`display:table`布局，问题文本标签使用`display:table-caption`用于改变元素的上下呈现位置，li元素的序号使用CSS计数器重现序号匹配，:optional伪类和:required伪类结合伪元素标记可行性，提升了维护性，主要代码如下

```html
<ol class="cs-ques-ul">
  <li class="cs-ques-li">
    <input type="radio" name="ques1" required>1-3年
    <input type="radio" name="ques1" required>3-5年
    <input type="radio" name="ques1" required>5年以上
    <!-- 标题后置 -->
    <h4 class="cs-caption">你从事前端几年了？</h4>
  </li>
  ...
  <li class="cs-ques-li">
    <textarea></textarea>
    <!-- 标题后置 -->
    <h4 class="cs-caption">有什么想说的？</h4>
  </li>
</ol>
```

```css
.cs-ques-li {
  display: table;
  width: 100%;
  counter-reset: quesIndex;
}
.cs-ques-li::before {
  counter-increment: quesIndex;
  content: counter(quesIndex) ".";
  /* 序号定位 */
  position: absolute;
  top: -.75em;
  margin: 0 0 0 -20px;
}
.cs-caption {
  display: table-caption;
  /* 标题显示在上方 */
  caption-side: top;
}
:optional ~ .cs-caption::after {
  content: "（可选）";
  color: gray;
}
:required ~ .cs-caption::after {
  content: "（必选）";
  color: red;
}
```

- 用户交互伪类:user-invalid和空值伪类:blank，:user-invalid用于用户显著交互后匹配不正确输入的元素，:blank规范也未成熟，使用:placeholder-shown替代

---

## 10. 树结构伪类

### :root伪类

- 在XHTML或HTML中:root伪类表示的就是html元素，需要IE9以上支持，:root值所有XML格式文档的根元素，对于SVG伪类:root就不是html标签了，Shadow DOM中的根元素使用:host伪类匹配
- 平常开发直接使用html标签选择器即可，在特定场景再使用:root伪类，如滚动条出现页面不跳动，页面高度超过一屏时滚动条显现会占据17px(window系统下)，使用`:root { overflow-x: hidden; } :root body { position: absolute; width: 100vw; overflow: hidden; }` 让浏览器计算宽度不包含滚动条
- 对于整站的颜色、主体布局尺寸等一般使用CSS变量定义在:root中，与html选择器分离开来u，html选择器赋值样式，:root负责变量

### :empty伪类

- 一般使用:empty伪类匹配空标签元素和前后闭合的替换元素，闭合标签内不能有注释、空格或换行，有则无法匹配，`::before和::after伪元素`可以给标签插入内容，但不影响:empty伪类的匹配

- 超高频使用的:empty伪类场景，如某一模块容器内的内容是动态的，容器本身有margin、padding等属性，有内容时显示正常但内容为空时会显示一块空白区域，可以使用:empty设置`display: none;`;字段缺失提示，跟上一场景类似只不过是将隐藏替换为无内容提示`.cs-empty:empty::before { content: '暂无数据'; display: block; }`，如可以用在表格某些字段缺失时使用占位文本示意`td:empty::before { content: '-'; color: gray; }`

### 子索引伪类

- :first-child和:last-child伪类分别匹配第一个和最后一个子元素，如可以优先使用:first-child列表项上下间距，使用:not伪类实现项间距更佳`li:not(:last-chid) { margin-bottom: 20px; }`
  
- :only-child伪类匹配无任务兄弟元素的元素，匹配时会忽略前后的文本内容，使用在动态数据场景，根据显示元素个数不同改变布局样式
  
- :nth-child()和:nth-last-chid()伪类，两者分别是从前面和后面按指定序号匹配，只适用于内容动态无法确定的场景，如果是静态数据直接使用类名和属性选择器更为简单；:nth-child()支持一个必填参数，为关键字odd(匹配第奇数个)、even(匹配第偶数个)及函数符号(An+B)，如`li:nth-child(n+4):nth-child(-n+10)`匹配第4~10个li元素，负数不匹配，正负数和奇偶数结合使用，如斑马线使用奇偶数匹配，表格前几行高亮区分显示使用正负数匹配间隔

- 动态列表数量匹配技术，根据伪类判断当前列表个数以自动失效不同列表数量的不同布局效果，如`li:first-child:nth-last-child(2)`判断共有两个li子元素，可以实现两个子元素一行显示，四个以上时九宫格布局显示等

### 匹配类型的子索引伪类

- :first-of-type和:last-of-type伪类分别匹配当前标签类型元素的第一个和最后一个

- :only-child伪类匹配唯一标签类型的元素

- :nth-of-type()和:nth-last-of-type()伪类分别从前面和后面匹配指定索引的当前标签类型元素，语法与:nth-child()类似，:nth-of-type()适用于特定标签组合且这些组合会不断重复的场景，如`dt+dd`和`details > summary`组合，还有同一容器下多组`input + label`组合的匹配，input元素隐藏且使用:nth-of-type()匹配label元素样式，无需再给input和label再嵌套一层标签

---

## 11. 逻辑组合伪类

### 否定伪类:not()

- :not()伪类匹配与括号内选择器不相符的元素，:not()本身优先级为0，最终选择器的优先级由括号内表达式决定，:not()伪类可以不断级联但不支持复杂的多表达式，只支持简单选择器，如`input:not(:disabled):not(:read-only)`

- :not()伪类最大应用场景是重置CSS样式，可以使代码简洁易读易维护，如禁用按钮:hover样式不生效`.cs-button:not(:disabled):hover { background-color: #eee; }`

### 了解任意匹配伪类:is()

- :any()是:matches()的前身，:matches()又是:is()伪类的前身，3个伪类语法一致，:is()更语义准确和简洁，其余两者已废弃，:is()本身优先级为0，整个选择器的优先级是由:is()参数中优先级最高的选择器决定

- :is()是新伪类，支持赋值选择器会选择器列表，如`:is(article:not([id]), section) p {  }`，目前有用但不迫切需要且未被浏览器全面支持

### 了解任意匹配伪类:where()

- :where()与:is()语法、作用一致，区别在于优先级不一样，:where()伪类优先级永远是0，参数内的选择器优先级被忽略，如`:where(#article) .content {}`优先级等同于.content选择器

---

## 12. 其他伪类选择器

### 与作用域相关的伪类

- 参考元素伪类:scope，除IE不支持外其余浏览器都已支持，网页中只有一个CSS作用域使用:scope等同于:root伪类，可以用于缺乏IE浏览器，在CSS中作用有限，但在DOM API中如`querySelector()、querySelectorAll()、matches()、closest()`，此时使用:scope伪类会从原本的页面作用域特性变成DOM API中指代的特定元素，如`document.querySelector('#myId').querySelectorAll(':scope div div');`

- Shadow树根元素伪类:host，Shadow DOM不受全局CSS影响，可以使用:host()伪类匹配Shadow DOM的根元素，:host()伪类对Web Components开放很重要，参数可以传递ID、类名或者属性进行匹配；:host-context()伪类也是用于匹配Shadow DOM根元素，与:host()区别在于其可以借助Shadow DOM根元素的父元素来匹配

### 与全屏相关的伪类:fullscreen

- 桌面浏览器和部分移动端浏览器支持原生全屏效果，通过element.requestFullScreen()让元素全屏显示，element.cancelFullScreen()取消全屏，如点击img元素图片进入全屏状态时使用:fullscreen匹配`:fullscreen .cs-img {}`

### 了解语言相关伪类

- 方向伪类:dir()，语法为`:dir(ltr | rtl)`，可以匹配元素设置了HTML dir属性或CSS direction属性的元素，用于改变元素布局方向，如国际化阿拉伯语镜像

- 语言伪类:lang()，用于匹配指定语言环境下的元素，如`.cs-share-zh:not(:lang(zh)), .cs-share-en:not(:lang(en)) { display: none; }`，借助:lang()伪类呈现不同语言环境下内容，伪类参数中的语言代码无需和HTML lang熟悉值一致，如`lang="zh-cmn-Hans"、lang="zh"`都可以使用:lang(zh)匹配

- 了解资源状态伪类，Video/Audio播放状态伪类:playing和:paused，目前还未得到浏览器支持，:playing用于匹配正在播放的音频元素，包括因为缓存而暂停的音频；:paused匹配处于停止状态的音频元素，包括处于明确停止状态和资源加载但未激活的元素

## 13. 总结

- 理解和思考选择器的使用，会帮助我们更好的完成界面交互效果，以及与HTML、JS解耦开来提升代码可维护性，书中有很多选择器应用场景的干货，需要自己去结合项目场景权衡使用，在实战中磨练提升用户体验
