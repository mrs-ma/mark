# Vuex

## 初始化vuex

Vuex 是一个专为 Vue.js 应用程序开发的  数据状态管理模式。

它采用集中式存储管理应用中  所有组件的数据 

Vuex是组件之间数据共享的一种机制

安装vuex

```
npm i vuex
```

main.js做如下设置

```
import Vue from 'vue'
import App from './App.vue'

// 1. 导入vuex
import Vuex from 'vuex'
// 2. Vue注册vuex
Vue.use(Vuex)
// 3. 实例化Vuex对象
const store = new Vuex.Store({
  // 通过state给vuex声明共享数据
  state: {
    count: 25, // 具体数据
    count1:26
  }
})

Vue.config.productionTip = false

new Vue({
  // 4. 挂载vuex
  store,
  render: h => h(App)
}).$mount('#app')

```

## 使用Vuex

### 访问state

```
this.$store.state.xxx   	// 组件内
$store.state.xxx 				// 模板中
```

### 修改(同步)mutations

```
// 在实例化Vuex对象的参数对象中，定义mutations成员(与state平级)对象，内部
// (mutations是与state平级的成员)
mutations:{
 	// 参数state是固定的，代表vuex本身的state，用以获取其中的共享数据
	方法名称(state,形参){
		通过state修改内部的数据
	}
}
```

`调用 mutations 语法`：

```
this.$store.commit('mutations方法名')
this.$store.commit('mutations方法名',实参)
```

### 修改(异步)actions

```
actions:{
  // context参数固定代表$store对象，
  // 可以调用commit等成员方法
  // 第二个参数可以接收应用层参数信息
  名称(context,形参){
    context.commit('mutations的方法名称', 参数)
  }
}

```

`调用语法`：

```
this.$store.dispatch('xx')
this.$store.dispatch('xx',参数)
```

# webpack

WebPack可以看做是模块**打包机器**,它做的事情是，分析你的项目结构，
找到JavaScript模块以及其它的一些浏览器不能直接运行的拓展语言
（less、es6、es7、vue等），一次性将它们打包为可供**所有浏览器**运行的合适的格式。

## 安装

```
npm i -D webpack webpack-cli
```

## 配置指令

打开 `package.json`文件，在 scripts 节点中，新增名称为 pack 的成员：

```
"scripts": {
  "build": "webpack"
}
```

依赖包的安装分为两种方式：开发 和 运行

依赖包在项目生产中充当**工具**作用的，建议通过开发依赖方式安装，例如webpack

依赖包在项目生产完毕**上线后都需要**使用的，就通过运行依赖方式安装，例如jquery

安装**运行**依赖包(dependencies)

```
npm i XXX  // 直接装包，没有任何其他参数，旧npm版本中要求设置--save参数例如jquery通过运行依赖方式安装npm i jquery
```

安装**开发**依赖包(devdependencies)

```
npm i XXX --save-dev // 设置额外参数--save-dev(简称为-D)
例如webpack等依赖包通过开发依赖方式安装
npm i --save-dev  webpack
```

在 src/index.js 入口文件中通过require(或es6 import)引入的就是运行依赖包，否则是开发依赖包

运行依赖和开发依赖包会分别配置到package.json的  **dependencies**和 **devdependencies** 段里边

## webpack配置

### 打包模式

在项目**根目录**中，新建一个 [webpack.config.js]() 配置文件，内容如下

```
module.exports = {
  mode: 'development'    // production    development
}
```

这是 使用 Node 语法， 向外导出一个 配置对象
production：打包的dist/main.js文件是优化、压缩的
development：打包的dist/main.js文件有适当的空白、换行、注释，可读性好

### 入口和出口配置

在[webpack.config.js]() 配置文件中也可以给其他参数做配置

```
module.exports = {
  entry: 'xxx',		//被打包的文件
  output:{
    path:'xxx',		//打包文件输出目录
    filename:'xxx',	//打包文件的名字
  }
}
```

## 构建模板页面

webpack默认情况下只对src/index.js文件打包，完毕后在html应用文件中手动引入使用，不够智能。

webpack打包src/main.js文件的同时也要去**打包** public/index.html 模板文件，并**生成**在 dist/index.html，同时**自动引入**对应的js出口文件

有一个名称为**html-webpack-plugin**的插件，可以帮助我们把html模板文件也打包到dist目录去，并在其中

**自动引入**js打包文件，然后dist/index.html就可以直接用于生产使用了

[参考官网](https://webpack.docschina.org/plugins/html-webpack-plugin)：

```
npm i html-webpack-plugin -D
```

去除js文件引入               在public/index.html中不需要引入任何js文件，打包后会**自动**引入

给webpack配置插件

在 [webpack.config.js]()中，导入 html-webpack-plugin 插件：

同时，把这个插件配置给plugins项目

```
const  HtmlWebpackPlugin  =  require('html-webpack-plugin')
plugins:  [
  new  HtmlWebpackPlugin({
    template:  'xxx'  // 被打包的html母模板文件路径名
  })
]
```

## 实时打包

webpack有一个名称为 **webpack-dev-sever** 工具，

这个工具可以**实时**处理js、**实时**处理html模板、**实时**编译查看效果，使得源代码随时变化，浏览器随时查看效果，显著提高开发效率

装包

```
npm i webpack-dev-server -D
```

在[webpack.config.js]()里边给webpack-dev-server配置运行参数

```
// 给实时打包工具webpack-dev-server做相关配置
devServer: {
  port: 19933, // 实时http服务端口配置
  host: '127.0.0.1', // 实时http服务主机ip地址配置
  open: true, // 自动启动浏览器并呈现相关效果
  compress: true // 以压缩方式传输网络内容
}
```

打开并配置package.json文件：

```
"scripts": {
  "serve": "webpack-dev-server"
}
```

现在使用如下指令就可以运行webpack-dev-server了

```
npm run serve
```

## loader

webpack本身就是一个**打包机器**，其不能对具体代码内容部分进行**处理**(或处理得非常有限)，不同的代码内容(less/scss/ES6(ES7)/image/css等等)需要webpack找到不同的 编译器 做码、编译、降级处理，这个编译器就是loader，中文为 装载器

| 不同内容 | loader处理器                                     |
| -------- | ------------------------------------------------ |
| css      | style-loader 和 css-loader                       |
| less     | less-loader 和 less(less是less-loader的内部依赖) |
| 图片     | url-loader 和 file-loader                        |
| ttf      | url-loader 和 file-loader                        |
| ES6/ES7  | babel-loader                                     |
| ...      | ...                                              |

### css

安装处理css的loader

```
npm i style-loader css-loader -D
```

配置loader

打开 [webpack.config.js]() 配置文件，在 module -> rules 数组中，新增处理 css 样式表的loader规则

```
module: { 
  // 制定各种类型文件的处理规则
  rules: [ 
    // css后缀文件loader匹配
    { 
      test: /\.css$/, 
      use: ['style-loader', 'css-loader'] }
  ]
}
```

打包好的css在哪

css的文件内容最终会被打包进 dist/bundle.js 出口文件中，浏览器运行就可以看到效果

 (原理：css文件内容被打包到bundle.js文件中，bundle.js文件运行时会创建**style标签**并填充css内容，之后这个style标签**嵌入**到应用文档里边)

### less

安装loader

```
npm i less-loader less -D
```

配置loader

在 [webpack.config.js]() 的配置文件中，新增一个 rules 规则来 处理 less 文件：

```
{ test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] }
```

打包好的less在哪

1. less的内容首先变为普通的css样式了 
2. 普通的css样式填充到bundle.js文件中

3. bundle.js文件运行创建style标签，体现的样式，嵌入文档生效

### 处理img文件

安装loader

```
npm i file-loader url-loader -D
```

配置loader

在 [webpack.config.js]() 的配置文件中，新增一个 rules 规则来 处理 img图片 文件

```
{
  // css样式中图片的处理loader设置
  test: /\.(png|jpg|gif)$/,
  use: [
    {
      loader: 'url-loader',
      options: {
        limit: 8192,
        outputPath: 'images'  // 现在做物理打包，图片就形成在dist/image目录里边了
      }                       (如果有多个图片都以物理文件形式被打包生成在dist目录，那么这个目录会显得                                非常凌乱，现在可以给loader做配置，使得图片生成在一个指定目录)
    }
  ]
}
```

图片在哪

大图被重新编译生成出来，位置是dist目录里边，并给重命名了

小图是通过**字符串**方式体现，被存储到bundle.js文件中
bundle.js运行的时候，通过style标签体现样式，进而体现小图背景效果

### 处理es6内容

webpack是打包工具，不是代码转换工具,用于降级es6或es7的loader名称为**babel-loader**

安装loader

```
npm i babel-loader @babel/core @babel/preset-env -D
```

配置loader

在 [webpack.config.js]() 的配置文件中，新增一个 rules 规则来 处理 es6高级语法内容

```
{
  // 通过loader对js文件中的es6/es7高标准进行降级处理，处理为es5
  test: /\.js$/,
  exclude: /node_modules/,设置表示对应目录不要经过babel-loader处理
  use: 'babel-loader'
}
```

在项目**根目录**创建[babel.config.js]()文件做如下配置

```
module.exports = {
  presets : ['@babel/preset-env'],
}
使得babel-loader找到preset插件集合帮忙处理es6/es7内容
```

### 处理ttf文件

字体库文件也需要配置loader做处理，具体与处理img图片的loader是一致的

### @别名和默认后缀

webpack.config.js中做如下配置

```
const ph = require('path')
module.exports = {
  resolve: {
    alias: {
      // 配置别名
      '@': ph.resolve('./src'),
    },
    // 配置自动识别后缀名
    extensions: [
      '.js',
      '.vue',
      '.json',
      '.css'
    ],
  },
}
```

