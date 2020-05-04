# Chrome DevTools 使用备忘录
> Chrome 开发者工具是一套内置于Google Chrome中的Web开发和调试工具，可用来对网站进行迭代、调试和分析。

> 打开Chrome 开发者工具，[键盘快捷键参考](https://developers.google.com/web/tools/chrome-devtools/shortcuts)
- 在Chrome菜单中选择 更多工具 > 开发者工具
- 在页面元素上右键点击，选择 “检查”
- 使用 快捷键 Ctrl+Shift+I (Windows) 或 Cmd+Opt+I (Mac)

## 元素面板 `Elements`
- 检查和编辑HTML与CSS
  - 左边三点或右键选中都可以弹出DOM操作的面板，如`Edit as HTML`(快捷键`F2`)可直接编辑HTML，`Hide element`(快捷键`H`)可隐藏DOM节点，`Copy element`(快捷键`Ctrl+C`)复制HTML，使用`Ctrl+V`粘贴，对DOM的修改可以使用快捷键`Ctrl+Z`和`Ctrl+Y`来进行撤销重做，对节点使用`Force state`可以方便的调试伪类样式，`Store as global variable`可以将DOM节点缓存到变量中。
  - `Styles`中可以寻找样式规则来源和实时编辑样式，`Ctrl + 点击属性(值)`可以快速转到源中属性(值)声明处	,其他[快捷键参考](https://developers.google.com/web/tools/chrome-devtools/shortcuts)。
  - `Computed` 检查和编辑当前元素的框模型参数,可用于定位当前元素生效样式来源。
  - `Event Listeners` 可以检查当前元素上绑定的事件(勾选Ancestor All查看所有祖先元素事件)，可以移除事件监听或是定位代码。
  - `DOM Breakpoints` 即监听右键选择元素`Break on`上的三个事件，`subtree modifications` 、`attribute modifications` 、`node remove`。
  - `Properties` 和 `Accessibility` 可以查看元素节点属性和可访问性属性。
![Elements检查元素操作](http://q8cyvs2hp.bkt.clouddn.com/Snipaste_2020-04-06_16-38-09.png)