# webpack

 > webpack 是一个现代 JavaScript 应用程序的静态模块打包工具  
 > 参考自[极客时间webpack专栏](https://time.geekbang.org/course/intro/100028901)和[webpack官网](https://www.webpackjs.com/concepts/)

## 基础

  webpack的基础概念和日常开放的使用技巧

  1. webpack与构建发展简史

     **为什么需要构建工具**

      - 转译ES Next语法
      - 转换JSX
      - CSS前缀补全/预处理器
      - 压缩混淆
      - 图片压缩

      **为什么选择webpack**

     - 社区生态丰富
     - 配置灵活和插件化扩展
     - 官方更新迭代速度快
  
  2. webpack基础用法

     webpack 默认配置文件为`webpack.config.js`，可以通过webpack --config 指定配置文件

     **entry**

     - 默认值是 `./src/index.js`
     - 可使用键值对声明多页面入口，webpack4会使用`optimization.splitChunks` 为页面间共享的应用程序代码创建 bundle

     **output**  

     - 默认值是 `./dist/main.js`，filename属性用于修改文件名，path属性用于修改文件输出路径，publicPath
     - 多入口需要使用`[name]`占位符确保每个文件具有唯一的名称，`[hash]`

     **loader**  

     - loader 让 webpack 能够去处理除JavaScript 和 JSON 文件外其他类型的文件
     - test 属性指定匹配规则， use 属性指定loader名称
     - 本身是个函数，接受源文件作为参数，返回转换结果，支持链式传递，按照相反的顺序执行，从右到左地取值(evaluate)/执行(execute)

     **plugin**  

     - require插件的模块路径后new实例插入plugin数组使用，插件用于执行范围更广的任务，优化bundle文件，如打包优化，资源管理，注入环境变量，作用于整个构建过程

     **mode**  

     - 可选值为 `development`、 `production` 、 `none` ，development、 production 会启用 webpack 内置在相应环境下的优化项，默认值为 production
     - 值设置为development会将DefinePlugin 中 process.env.NODE_ENV 的值设置为 development，
     - 值设置为 production 会将DefinePlugin 中 process.env.NODE_ENV 的值设置为 production

  3. webpack进阶用法  

      **loader解析文件**

     - 解析JS
       [babel-loader](https://webpack.docschina.org/loaders/babel-loader/)转译 JavaScript 文件，可以在`.babellrc`配置文件使用 options 属性配置presets和plugins来转译ES6或解析JSX语法
     - 解析CSS
       [css-loader](https://webpack.docschina.org/loaders/css-loader/)用于加载.css文件并转换为commonjs对象  
       [style-loader](https://webpack.docschina.org/loaders/style-loader/)将样式通过`<style>`标签插入到head中
       [postcss-loader](https://webpack.docschina.org/loaders/postcss-loader/)后处理器用于自动补齐CSS属性前缀
       [sass-loader](https://webpack.docschina.org/loaders/sass-loader/)预处理器，将Sass 编译成 CSS
     - 解析字体、图片等媒体资源  
       [file-loader](https://webpack.docschina.org/loaders/file-loader) 生成到输出目录，并返回文件的 public URI  
       [url-loader](https://webpack.docschina.org/loaders/url-loader) 像 file loader 一样工作，还可以配置文件大小限制返回 base64 数据

     **文件指纹**

     - 通常用于文件版本管理
     - 生成方式
       Hash：与项目构建相关，项目文件有修改则项目构建时hash会更改，如用于图片文件输出name使用`[hash]`  
       Chunkhash：与webpack打包chunk相关，entry不同则生成不同chunkhash值，如使用CSS文件指纹  
       Contenthash：根据文件内容定义hash，文件内容不变则contenthash不变，如用于JS文件output.filename中`[contenthash:8]`

## 进阶

  以工程化的方式组织webpack构建配置和打包webpack优化
  **30 | Scope Hoisting使用和原理分析**

  1. 编写可维护的webpack构建配置
  2. webpack构建速度和体积优化策略

## 原理

  剖析webpack打包原理、插件及loader的实现

  1. 通过源码掌握webpack打包原理
  2. 编写Loader和插件

## 实战

  从实际Web商城项目出发讲解webpack实际使用

  1. React全家桶和webpack开放商城项目
