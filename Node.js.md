# Node.js

## 在node环境下运行js代码

前面的学习中，js代码都是在浏览器中运行的，现在开始学习nodejs后，我们有了第二个环境中可以运行js代码。

有两种方式可以运行js代码：

- 在nodejs 提供的repl中环境
- 单独执行外部的js文件

方法1：在 REPL中运行（了解）

REPL(Read Eval Print Loop:交互式解释器) 表示一个电脑的环境，类似 Window 系统的终端或 Unix/Linux shell，我们可以在终端中输入命令，并接收系统的响应。

Node 自带了交互式解释器，可以执行以下任务：

- **读取** - 读取用户输入，解析输入了Javascript 数据结构并存储在内存中。
- **执行** - 执行输入的数据结构
- **打印** - 输出结果
- **循环** - 循环操作以上步骤直到用户两次按下 **ctrl-c** 按钮退出。

具体操作：

1. 在任意控制台中输入node 并回车确定，即可进行入node自带的REPL环境。
2. 此时，你可以正常写入js代码，并执行。
3. 如果要退出，**连续按下两次ctrl+c**

方法2：执行一个JS文件（常用）

1. 请事先准备好一个js文件。
   - 例设这的路径是：e:/index.js
   - 具体内容是

```javascript
var a = 1;
console.info(a + 2);
```

2. 打开小黑窗，进入到这个文件的目录
   - 技巧，在资源管理器中按下shift，同时点击鼠标右键，可以选择在此处打开powershell窗口。
   - cd 命令可以用来切换当前目录。
3. 接下来 通过  ` node js文件的路径 `   的格式来执行这个js文件。

```javascript
node index.js
```

注意:

- 执行js文件时，如果当前命令行目录和js文件**不在**同一个盘符下，要先**切换盘符**
  - 切换方式，输入`盘符:`并回车
- 如果当前命令行目录和js文件**在**同一个盘符中，则可以使用**相对路径**找到js文件并执行

## node.js是什么

- Node全名是Node.js，但它不是一个js文件，而是一个软件
- Node.js是一个**基于Chrome V8引擎**的**ECMAScript的运行环境**，在这个环境中可以执行js代码
- Node.js提供了大量的工具（API），能够让我们完成文件读写、Web服务器创建等功能

### nodejs和浏览器和javascript的关系

nodejs和浏览器的关系:

相同之处：

- 都可以运行js(严格来讲是ECMAScript)代码

不同之处：

![1562665535479](D:/就业班/就业班第34天nodejs/01_资料/讲义/2-nodejs/node-material.assets/1562665535479.png)

- 安装了浏览器这个软件，它不但可以执行**ECMAScript**，浏览器这个软件内置了window对象，所以浏览器有处理**DOM和BOM**的能力。
- 安装了NodeJs这个软件，它不但可以执行**ECMAScript**，NodeJS这个软件也内置了一些功能，包括**全局成员和模块系统**，同时还可以载**入第三方模块**来完成更强大的功能。

nodejs和javascript的区别？

- nodejs是一个容器（不是一个新语言），ECAMScript程序可以在这个容器中运行。
  - 不能在nodejs使用window对象，也不能在nodejs使用dom操作。因为nodejs中并不包含这个对象。
- javascript是由三个部分组成：ECMAScript,BOM,DOM

# nodejs中的模块

每个模块都是一个独立的文件。每个模块都可以完成特定的功能，我们需要时就去引入它们，并调用。不需要时也不需要要管它。（理解于浏览器的js中的Math对象）

nodejs模块的分类

- **核心模块** (类似内置对象Array Math Date...)
  - 就是nodejs**自带的模块**，在安装完nodejs之后，就可以随意使用啦。相当于学习js时使用的内置对象。
  - 全部模块的源代码 https://github.com/nodejs/node/tree/master/lib
- **自定义模块** (类似config.js user.js  common.js)
  - 程序员自己写的模块。就相当于我们在学习js时的自定义函数。
- **第三方模块** (jQuery template-web.js )
  - 其他程序员写好的模块。nodejs生态提供了一个专门的工具来管理第三方模块。
  - 相当于别人写好的函数或者库。例如我们前面学习的jQuery库，artTemplate等

## fs模块(核心模块)

fs模块是文件操作模块。fs是 FileSystem的简写。它用来对文件，文件夹进行操作。

```
const fs = require('fs');
```

fs模块中操作文件(或者文件夹)的方法，大多都提供了两种选择：

- 同步版本的
- 异步版本的

### 文件内容读取 - readFile

异步格式:

```
fs.readFile('文件路径'[,选项], (err, data) => {
  if (err) throw err;
  console.log(data);
});
- 第一个参数：文件路径。 相对路径和绝对路径均可。
- 第二个参数： 配置项，可选参数。主要用来配置字符集。一般可设置为'utf8'

      如果不设置该参数，文件内容会以二进制形式返回。

- 参数3: 读取完成后触发的回调函数。有两个参数 --- err 和 data
  - 读取成功
    - err: null
    - data: 文件内容，如果不设置参数2,则返回二进制数据。可以使用 toString() 方法将二进制数据
      转为正常字符串
  - 读取失败
    - err: 错误对象
    - data: undefined

```

同步格式

```
const fs = require("fs")
let rs = fs.readFileSync('文件路径',"utf8");
console.log(rs)

与异步格式不同在于：
- api的名字后面有Sync
- 不是通过回调函数来获取值，而是像一个普通的函数调用一样，直接获取返回值

```

### 文件写入(覆盖写入 writeFile)

功能：向指定文件中写入字符串（覆盖写入）， 如果没有该文件则尝试创建该文件。它把把文件中的内容全部删除，再填入新的内容。

格式：`fs.writeFile(var1, var2, var3, var4);`

参数1: 要写入的文件路径 --- 相对路径和绝对路径均可，推荐使用绝对路径

参数2: 要写入文件的字符串

参数3: 配置项，设置写入的字符集，默认utf-8

参数4: 写入完成后触发的回调函数，有一个参数 --- err （错误对象）

```
const fs = require('fs')
fs.writeFile('./a.txt', 'hello world niahi \n asfsdf', err => {
  if (err) {
    console.info(err)
    throw err
  }
})
```

### 文件追加 appendFile

功能 ：向指定文件中写入字符串（追加写入）， 如果没有该文件则尝试创建该文件

格式：`fs.appendFile(var1, var2, var3, var4);`

参数1: 要写入的文件路径 --- 相对路径和绝对路径均可，推荐使用绝对路径

参数2: 要写入文件的字符串

参数3: 配置项，设置写入的字符集，默认utf-8

参数4: 写入完成后触发的回调函数，有一个参数 --- err （错误对象）

```
const fs = require('fs')

fs.appendFile('./a.txt', '\n 为天地立命', err => {
  if (err) {
    console.info(err)
    throw err
  }
})
```

### fs模块中的常用方法

| API                                         | 作用              | 备注           |
| ------------------------------------------- | ----------------- | -------------- |
| fs.access(path, callback)                   | 判断路径是否存在  |                |
| fs.appendFile(file, data, callback)         | 向文件中追加内容  |                |
| fs.copyFile(src, callback)                  | 复制文件          |                |
| fs.mkdir(path, callback)                    | 创建目录          |                |
| fs.readDir(path, callback)                  | 读取目录列表      |                |
| fs.rename(oldPath, newPath, callback)       | 重命名文件/目录   |                |
| fs.rmdir(path, callback)                    | 删除目录          | 只能删除空目录 |
| fs.stat(path, callback)                     | 获取文件/目录信息 |                |
| fs.unlink(path, callback)                   | 删除文件          |                |
| fs.watch(filename[, options]\[, listener])  | 监视文件/目录     |                |
| fs.watchFile(filename[, options], listener) | 监视文件          |                |
| fs.existsSync(absolutePath)                 | 判断路径是否存在  |                |

## 路径问题

在读取文件时，写相对路径是容易出问题的.

nodejs中提供了两个全局变量来获取获取绝对路径

- __dirname：获取当前被执行的文件的文件夹所处的绝对路径
- __filename：获取当前被执行的文件的绝对路径

## path模块(核心模块)

它是一个核心模块，用来处理路径问题：拼接，分析，取后缀名

- path.basename（路径）获取
- **path.join()**  （常用）
- path.parse(path) 转成一个对象

path模块其它方法列表:

| path.basename(path[, ext]) | 获取返回 path 的最后一部分(文件名) |
| -------------------------- | ---------------------------------- |
| path.dirname(path)         | 返回目录名                         |
| path.extname(path)         | 返回路径中文件的扩展名(包含.)      |
| path.format(pathObject)    | 将一个对象格式化为一个路径字符串   |
| path.join([...paths])      | 拼接路径                           |
| path.parse(path)           | 把路径字符串解析成对象的格式       |
| 方法                       | 作用                               |
| path.resolve([...paths])   | 基于当前工作目录拼接路径           |

## http模块(核心模块)

我们能够通过简单的代码创建一个Web服务器，处理http请求。

### 快速搭建Web服务器

1.新建文件，写入如下代码。

```
// http.js
// 引入核心模块http
const http = require('http');

// 创建服务
const server = http.createServer(function(req, res) {
  console.log(req.connection.remoteAddress);
  res.end('hello world');
});
其中的参数是一个函数，这个函数是一个匿名函数，这个函数充当回调函数的角色，当有http请求时，它会自动被调用。
这个回调函数有它有两个参数。这两个参数非常重要，也非常复杂.

- 第一个参数表示来自客户端浏览器的请求，第二个参数用来设置对本次请求的响应。它们的形参名并不重要，但是，一般第一个参数名使用req或者request表示，第二个参数使用res或者resposne表示。
- 当某个客户端来请求这个服务器时，这个函数会自动调用，同时会自动给这两个参数赋值。第一个参数中包括本次请求的信息。
  - req：请求
    - req.url。本次请求的地址
    - req.method。   获取请求行中的请求方法
    - req.headers。    获取请求头
- 第二个参数用来设置本服务器对这次请求的处理。
  - 这个参数一般命名是res，它是一个对象，其中有很多方法和属性。
  - res.end() 
    - 把把本次的处理结果返回给客户端浏览器
    - 如果不写这一句，则客户端浏览器永远收不到响应。
  - res.setHeader()  设置响应头，比如设置响应体的编码
    res.setHeader('content-type', 'text/html;charset=utf-8');
  - res.statusCode 设置状态码

// 启动服务
server.listen(8081, function() {
  console.log('success');
});
```

2.运行代码, `node http.js`

3.在浏览器地址栏中输入：localhost:8081 观察效果。

### http模块-处理静态资源

静态资源指的是html文件中链接的外部资源，如css、js、image文件等等。

**处理二次请求**

从服务器获取html文件之后，如果这个html文件中还引用了其它的外部资源（图片，样式文件等），则浏览器会重新再发请求。

假设在index.html中还引入了 style.css 1.png 或者 .js文件，则：

浏览器请求localhost:index.html之后，得到的从服务器反馈的内容，解析的过程中还发现有外部的资源，所以浏览器会再次发出第二次请求，再去请求相应的资源。

一个最朴素的想法是根据不同的请求来返回不同的文件。

```
const http = require('http');
const fs = require('fs');
const path = require('path');

//创建服务器
const app = http.createServer((req, res) => {

  if (req.url === '/index.html') {
    let htmlString = fs.readFileSync(path.join(__dirname, 'index.html'));
    res.end(htmlString);
  }
  else if (req.url === '/style.css') {
    let cssString = fs.readFileSync(path.join(__dirname, 'style.css'));
    res.setHeader('content-type', 'text/css');
    res.end(cssString);
  } else if (req.url === '/1.png') {
    let pngString = fs.readFileSync(path.join(__dirname, '/1.png'));
    res.end(pngString);
  } else {
    res.setHeader('content-type', 'text/html;charset=utf-8');
    res.statusCode = 404;
    res.end('<h2>可惜了, 找不到你要的资源' + req.url + '</h2>');
  }
}); 
//启动服务器，监听8082端口
app.listen(8082, () => {
  console.log('8082端口启动');
});
```

**为不同的文件类型设置不同的 Content-Type**

通过使用res对象中的setHeader方法，我们可以设置content-type这个响应头。这个响应头的作用是告诉浏览器，本次响应的内容是什么格式的内容。以方便浏览器进行处理。

常见的几中文件类型及content-type如下。

- .html：` res.setHeader('content-type', 'text/html;charset=utf-8') `
- .css：`res.setHeader('content-type', 'text/css;charset=utf-8')`
- .js：`res.setHeader('content-type', 'application/javascript') `
- .png：`res.setHeader('content-type', 'image/png')`

**批量处理请求**

由于我们不法事先得知一个.html文件中会引用多少个静态资源，所以，我们不能像处理某个页面一样去处理它们。我们的解决办法有两大类是：

1. 把这类静态资源连同所有的.html文件全放在固定的文件夹中。在用户请求时，当判断当前的req.url是在这个文件夹下就是直接读内容，并返回。

   2.分析后缀名，如果是允许的，就直接返回

### http模块-实现接口功能

get类型的接口-无参数

地址：/gettime

功能：以json字符串格式返回服务器的时间戳。

```
const http = require('http');
const app = http.createServer((req, res) => {
  if (pathname === '/gettime') {
    let obj = {_t : Date.now()}
    res.end(JSON.stringify(obj));//  把对象转成字符串之后再返回
  } else {
    res.end('error');
  }
});
app.listen(8083, () => {
  console.log(8083);
});

说明：

- req.method 可以判断请求的类型
- res.end()的参数只能是字符串，而不能是对象

```

**接口与静态资源的区别**:

服务器上有很多的资源，每个资源都有自己的url。客户端浏览器想要访问某个资源就要向服务器发起对应的请求。

资源的分类：

- 静态资源。
  - 它们一般表现为一个一个的**文件**。例如index.html, style.css, index.js。
  - 处理请求静态资源时，服务器一般就直接读出资源的内容，再返回给客户端浏览器
- 动态资源：接口
  - 它们不是以某个具体的文件存在的，而是通过服务器上的一段代码处理得到的**数据**，访问接口时，服务器会执行这段代码，然后把代码的执行结果返回给客户端浏览器。

## url模块(核心模块)

作用:url模块用来对url（例如：http://tmall.cn:80/clothes/women?id=18&name=zs#photo）进行解析，进而得到各种信息。

```
let urlobj = url.parse(req.url); // urlobj对象中，就有我们需要的信息
urlobj.pathname :获取用户输入的url的路径名 ('/clothes/women')
urlobj.search: '?id=18&name=zs',
urlobj.query: 获取用户输入的url中的查询字符串( 'id=18&name=zs' )
urlobj.path: '/clothes/women?id=18&name=zs',
urlobj.href: '/clothes/women?id=18&name=zs' 
```

## querystring模块(核心模块)

用来对url中的查询字符串这部分进行处理。nodejs中提供了querystring这个核心模块来帮助我们处理这个需求。

```
const qs= require('querystring');
let obj = qs.parse('id=18&name=zs');
console.log(obj)
```

**get类型的接口-带参数**

```
const http = require('http');
const queryString = require('querystring');
const url = require('url');

const server = http.createServer(function(req, res) {
  var { pathname, query } = url.parse(req.url);
  var obj = queryString.parse(query);

  console.log(p, url.parse(req.url));
  if (pathname === '/get' && req.method === 'GET') {
    res.setHeader('content-type', 'application/json');
    obj.d: Date.now() };
    res.end(JSON.stringify(str));
  } else {
    res.setHeader('content-type', 'text/html;charset=utf-8');
    res.end('大家好');
  }
});
server.listen(8088, function() {
  console.log('success', 8088);
});
```

**post接口**

```
接口地址:localhost:8080/post
参数：name=filex&age=30;
返回:{name:filex,age:30,_t:1563265441778}
```

post类型与get类型的接口区别较大，主要在两个方面：

1. 类型不同

   对于类型不同还比较好判断，我们可以通过 req.method 来获取

2. 传参不同

   - get请求参数在请求行中（附加在url后面）
   - post请求参数在`请求体`中

对于获取post参数就相对复杂一些，主要是用到request对象的两个事件data,end。

基本流程是：

1. 在req对象上添加两个事件，用来收集参数

   1. req.on("data",function(chunk){ })

      每次收到一部分数据就会触发一次这个事件，回调函数也会相应的执行一次。其中的chunk是一个形参（你也可以换个参数名），它是一个buffer。

   2. req.on("end",function(){})

2. 解析参数

```
const http = require('http');
const url = require('url');
const queryString = require('querystring');
const server = http.createServer(function(req, res) {
  var { pathname } = url.parse(req.url);
  if (pathname === '/post' && req.method === 'POST') {
    let data = '';
    req.on('data', chunk => {
      data += chunk;
    });
    req.on('end', () => {
      res.setHeader('content-type', 'application/json');
      var str = { ...queryString.parse(data), d: Date.now() };
      res.end(JSON.stringify(str));
    });
  } else {
    res.setHeader('content-type', 'text/html;charset=utf-8');
    res.end('大家好');
  }
});

server.listen(8088, function() {
  console.log('success', 8088);
});
```

# 自定义模块

我们自己写的模块就是自定义模块。在nodejs中 ，我们对代码的封装是以模块（一个一个的文件）为单位进行的。一般的做法是实现好某一个功能之后，封装成一个模块，然后在其它文件中使用这个模块。

使用一个模块，就是一个js文件中去使用另一个js文件中定义的变量，常量，函数....

## 基本步骤

1.定义模块

新建一个js文件，用模块名给它命名。例如，你的模块叫myModule，则这个js文件最好叫myModule.js

2.导出模块

在myModule.js内部，我们定义一些函数，变量，当然，它们会根据我们的业务要求做一些不同的工作。最后根据情况导出这些函数，变量。

```
//myModule.js
const myPI = 3;
function add(a, b) {
  return a + b;
}
// 通过module.exports来导出
module.exports = {
  myPI,
  add
};
```

注意：

- module.exports 是固定写法，一般放在文件的最末尾，也只用一次。
- module.exports表示当前模块要暴露给其它模块的功能。你当然不必须要所有在模块中定义的函数都暴露出来。

3.引入模块

在你需要使用模块的文件中，使用require语句引入你定义好的模块，注使用相对路径。假设我们当前的文件是index.js，而我们希望在index.js文件中使用myModule.js中的add方法。

我们的做法是：

```
// index.js
const myMath = require('./myMath');

上面的require()就是用来引入模块的。这里要注意使用自定义模块时，使用相对路径，而使用核心模块时，不需要写路径。
```

4.使用模块

当一个模块被成功引入之后，就可以按使用核心模块的过程一样去使用它们了。

# npm使用

nodejs通过自带的`npm`(node package manager)工具来管理第三方模块，所以，在学习使用第三方模块时，我们先要学习npm的使用。

- `npm` 全称 `Node Package Manager`(node 包管理器)，它的诞生是为了解决 Node 中第三方包共享的问题。
- `npm` 不需要单独安装。在安装Node的时候，会连带一起安装`npm`。

## 包（package）与模块关系

nodejs中一个模块就是一个单独的js文件

- **包是多个模块的集合**。一个模块能够解决的问题比较单一，一个包中有多个模块。
- npm 管理的单位就是包

类似于网站和网页的区别：一个网站一般会包含多个网页。

## 通过npm命令行下载第三方模块（包）

分成三步：

- 初始化项目。如果之前已经初始化，则可以省略(npm init --yes 或者是 npm init -y)
- 安装包。 **npm install 包名**
- 引入模块，使用。

全局安装包和本地安装包:

- 全局安装: 包被安装到了系统目录（一般在系统盘的node_modules中），本机都可以使用使用。

  - 命令：`npm install -g 包名`

- 局部安装（或者叫本地安装)，包并安装在当前项目的根目录下，与package.json同级目录的node_modules。就只在这个项目中可以使用。

  - 命令：`npm install 包名`

# Express框架

## Express 介绍

- Express 是一个基于 Node.js 平台，快速、开放、极简的 **web 开发框架**
- Express 是一个第三方模块，有丰富的 API 支持，强大而灵活的**中间件**特性
- Express 不对 Node.js 已有的特性进行二次抽象，只是在它之上扩展了 Web 应用所需的基本功能

## 运行一个express程序

安装:

```
# 在你的项目根目录下，打开小黑窗

# 1. 初始化 package.json 文件
npm init -y

# 2. 本地安装 express 到项目中
# npm install express
npm i express
```

使用:

在项目根目录下新建一个js文件，例如app.js，其中输入代码如下

```
// 0. 加载 Express
const express = require('express')

// 1. 调用 express() 得到一个 app
//    类似于 http.createServer()
const app = express()

// 2. 设置请求对应的处理函数
//    当客户端以 GET 方法请求 / 的时候就会调用第二个参数：请求处理函数
app.get('/', (req, res) => {
  res.send('hello world')
})

// 3. 监听端口号，启动 Web 服务
app.listen(3000, () => console.log('app listening on port 3000!'))

res.send()是exprss提供的方法，用于结束本次请求。类似的还有res.json(),res.sendFile() 。
```

### 托管静态资源:

```
// 0. 加载 Express
const express = require('express')

// 1. 调用 express() 得到一个 app
//    类似于 http.createServer()
const app = express();

// 2. 设置请求对应的处理函数
app.use(express.static('public'))


// 3. 监听端口号，启动 Web 服务
app.listen(3000, () => console.log('app listening on port 3000!'))

此时，所有放在public下的内容可以直接访问，注意，此时在url中并不需要出现public这级目录
- 在public下新建index.html。可以直接访问到。

app.use('/public', express.static('public'))
这意味着想要访问public下的内容，必须要在请求url中加上/public
```

### 写get接口

get无参数:

```
const express = require('express');
const app = express();
app.get('/get', function(req, res) {
  // 直接返回对象
  res.json({ name: 'abc' });
});
app.listen('8088', () => {
  console.log('8088');
});
```

get有参数:

```
const express = require('express');
const app = express();
app.get('/get', function(req, res) {
  // 直接返回对象
  console.log(req.query);
  
  res.send({ name: 'abc' });
});
app.listen('8088', () => {
  console.log('8088');
});
```

### 写post接口

无参数:

```
const app = express();
app.post('/post',function(req,res){
	res.send({name:"abc"})
})
```

普通键值对参数:

获取post普通键值对数据，要通过第三方模块`body-parser`来解析。

具体来说当content-type为x-www-form-urlencoded时，表示上传的普通简单的键值对

```
npm install body-parser

// 1. 引入包
const bodyParser = require('body-parser');

// 2. 使用包
app.use(bodyParser.urlencoded({extended:false}));

app.post("/add",function(req,res){

    //3. 可以通过req.body来获取post传递的键值对	

})

app.use(....)之后，在res.body中就会多出一个属性res.body。
```

### 文件上传

如果post涉及文件上传操作，则会要使用`multer`这个包来获取上传的信息。

```
npm install multer
// 1. 引入包
const multer = require('multer');
// 2. 配置
const upload = multer({dest:'uploads/'}) // 上传的文件会保存在这个目录下
uploads表示一个目录名，你也可以设置成其它的

// 3. 使用
// 这个路由使用第二个参数 .upload.single表示单文件上传， 'cover' 表示要上传的文件在本次上次数据中的键名。类似于<input type="file" name='cover'/>

app.post("postfile",upload.single('cover'), function(req,res){

})
```

# 中间件技术

中间件**是**一个特殊的url地址处理**函数**,一个 express 应用，就是由许许多多的中间件来完成的

```
// 具名函数格式：
const handler1 = (req, res, next) => {
  console.log(Date.now());
  next();
}
app.use(handler1);

// 匿名函数格式：
app.use((req, res, next) => {
  console.log(Date.now());
  next();
});
```

- 中间件本质就是一个函数，它被当作 `app.use(中间件函数)` 的参数来使用
- 中间件函数中有三个基本参数， req、res、next
  - req就是请求相关的对象，它和下一个中间件函数中的req对象是一个对象
  - res就是响应相关的对象，它和下一个中间件函数中的res对象是一个对象
  - next：它是一个函数，调用它将会跳出当前的中间件函数，执行中间件；如果不调用next，则整个请求都会在当前中间件卡住，而得不到返回。

# 会话控制

会话控制就是用来弥补http无记忆的缺陷的一种技术。它能够将数据持久化（保存数据）的保存在客户端(浏览器)或者服务器端，从而让浏览器和服务器进行多次数据交换时，产生连续性。

让每一次的请求和响应都知道对方是谁。

- cookie： 将数据保存到**客户端**（浏览器）
- session： 将数据保存到**服务器端**

