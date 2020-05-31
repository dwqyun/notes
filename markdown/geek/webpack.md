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

     **为什么需要构建工具**

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

     - require插件后new实例插入plugin数组使用，插件用于执行范围更广的任务，优化bundle文件，如打包优化，资源管理，注入环境变量，作用于整个构建过程
     **mode**  

     - 可选值为 `development`、 `production` 、 `none` ，development、 production 会启用 webpack 内置在相应环境下的优化项，默认值为 production
     - 值设置为development会将DefinePlugin 中 process.env.NODE_ENV 的值设置为 development，
     - 值设置为 production 会将DefinePlugin 中 process.env.NODE_ENV 的值设置为 production

  3. webpack进阶用法

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
