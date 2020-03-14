# URL的基本概念

URL概念：统一资源定位符 （UniformResourceLocator）

- 俗称网址，用来标识某个资源在网络中的唯一位置。

通信协议： https://

域名（服务器地址）： detail.tmall.com

资源的具体位置：  /item.htm?id=555428842095&spm=a310p.7395781.1998038982.3

# AJAX简介

> Ajax（**Async**hronous Javascript And XML（异步 JavaScript 和 XML））

- 作用：用来发送请求的一种方式
- 实现方式简介：浏览器提供了一个XMLHttpRequest的构造函数，创建的对象用来进行ajax操作
- 特点：无需刷新页面，也可以进行请求响应处理（局部刷新）

**常见异步任务有哪些：**

- 定时器
  - 示例：无论定时器的时间为多少，都会比同步任务执行晚。
- Ajax

- **执行顺序：异步任务的执行一定晚于同步任务**

## $.get()的使用

没有请求参数，接收响应数据

```
$.get(地址, function(res) {
  // 响应接收完毕后，执行回调函数
  // res代表响应的数据，如果res为JSON格式，jQuery会自动转换
});
```

有请求参数，接收响应数据  请求参数：请求中发送给服务端的数据

```
$.get(地址, 请求参数组成的对象, 回调函数);
```

## $.post()的使用

有请求参数，接收响应数据  请求参数：请求中发送给服务端的数据

```
$.post(地址, 请求参数组成的对象, 回调函数);
```

## $.ajax()的使用

type表示请求方式，默认为'GET'，可以设置为'GET'/'POST'

url表示请求地址   只有url属性是必须设置的

data表示请求参数，对象结构

success表示响应成功时的处理函数(res参数，表示响应内容)

# 表单和ajax结合使用

在submit事件中，设置e.preventDefault()方法即可(推荐)， return false也可以阻止表单的默认提交行为

## jQuery的serialize方法

可以快速获取表单中的所有数据(**只能获取纯文本数据**)

使用方式： $(form的选择器).serialize() 

- 结果形式：
  - 名=值&名=值&名........
- 注意：这种内容格式可以通过$.get $.post $.ajax进行直接发送
  - 注意表单元素如果没有name，数据是无法正确提交的

# 模板引擎

## 使用步骤

1.引入template-web.js

2.准备数据(通常为请求得到的数据)

3.准备模板

​    使用script标签，设置type为text/template，设置id

​    内部书写需要的结构内容

​    结合模板语法进行操作

4.调用template方法处理

​     template('id名', 数据)

​     返回值为将数据和模板结合后得到的字符串

## 模板引擎的语法

{{数据}}基本值的访问方式

{{}} 是模板的基本标记，标记中会进行模板语法的执行，标记外原样输出

{{$data}} 代表template()的参数2

{@数据}}  如果数据中含有html标签结构，可以生成，如果不加@就不会生成

模板中的if使用

```
  {{if age>=18}}
    <p>此人成年了</p>
    {{else}}
    <p>此人未成年</p>
    {{/if}}

    {{if age===17}}
    <p>此人17岁</p>
    {{/if}}

    {{if age===21}}
    <p>此人21岁</p>
    {{else if age===20}}
    <p>此人20岁</p>
    {{else}}
    <p>此人不知道多少岁</p>
    {{/if}}
```

{{each}} 模板数据遍历

- 可以统一遍历数组和对象两种形式
- 在each中$index和$value是模板默认提供的名称， $index代表索引/属性名  $value代表元素值/属性值
- 可以通过自定义名称替换$index与$value

```
  	{{each aiHao}}
      <div>这是div</div>  {{$index}}   {{$value}}
    {{/each}}

    {{each aiHao v i}}
      <div>这是div</div> {{v}} {{i}} 
    {{/each}}


    {{each obj}}
    <p>这是p标签</p>  {{$index}}   {{$value}}
    {{/each}}

    {{each obj value key}}
    <p>这是p标签</p>  {{key}}   {{value}}
    {{/each}}

```

## 模板的过滤器功能

作用：是用来对模板中某些数据进行处理的一个方法

设置方式：**在调用模板功能前设置**

```
template.defaults.imports.过滤器名称 = function (模板中书写的数据) {
  // 进行各种的内容处理
  return '处理结果';
};
```

过滤器的返回值，会作为模板中最终展示的数据

模板中的写法

```
{{time}}  这是普通的输出方式
{{time|过滤器名称}} 这是通过过滤器处理后的输出方式
```

# 原生Ajax使用

## get请求基本使用

**步骤：**

1. 创建xhr对象

2. 调用open：设置请求方式和请求地址

3. 调用send: 发送请求（这一步是异步操作）

4. 设置onreadystatechange事件，监听请求的各种状态

   - readyState是xhr的属性，用来表示请求发送的状态
     - 取值为4代表下载完毕

     - 必须确保readyState为4才能使用响应的数据

   - xhr.status 代表请求是否成功

     - 200代表请求是成功的

   - xhr.responseText 代表接收的响应内容

```
// 1 创建xhr对象
    var xhr = new XMLHttpRequest();
    // 2 调用open：设置请求方式和请求地址
    xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks');
    // 3 调用send: 发送请求，这一步是异步操作
    xhr.send();

    // 4 设置事件，监听请求的各种状态
    //   - readyState是xhr的属性，用来表示请求发送的状态
    //     - 取值为4代表下载完毕
    //     - 必须确保readyState为4才能使用响应的数据
    //     - 进一步检测：
    //       - xhr.status 代表请求是否成功
    //          - 200代表请求是成功的
    xhr.onreadystatechange = function () {
      // 4.1 检测xhr.readyState取值和xhr.status取值
      if (xhr.readyState === 4 && xhr.status === 200) {
        // 4.2 接收响应的数据即可
        //    - 原生接收的响应内容是JSON格式，需要自己进行转换
        //      - jQuery会自动转换
        console.log(xhr.responseText);
      }
    };
```

## 带有参数的get请求

- 书写方式：
  - **位置：在xhr.open()的参数2 url后面书写参数内容**
  - 名称：参数的形式称为**查询字符串**
  - 格式：  ?名=值&名=值...
    - 其中  名=值&名=值...  称为**url编码格式，英文为urlencoded**
- jQuery的get请求和原生get请求的**本质是一样**的

```
// 1 创建xhr对象
    var xhr = new XMLHttpRequest();
    // 2 调用open：设置请求方式和请求地址
    //    - 如果希望设置get请求的请求参数，需要放置在open()参数2地址的最后位置
    //    - 书写方式为：  地址?名=值&名=值....
    //    - 名称说明： 名=值&名=值称为url编码格式  urlencoded
    xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks?id=3&name=jack&age=18');
    // 3 调用send: 发送请求，这一步是异步操作
    xhr.send();

    // 4 设置事件，监听请求的各种状态
    xhr.onreadystatechange = function () {
      // 4.1 检测xhr.readyState取值和xhr.status取值
      if (xhr.readyState === 4 && xhr.status === 200) {
        // 4.2 接收响应的数据即可
        console.log(xhr.responseText);
      }
    };
```

## post请求的发送方式

步骤：

1. 创建xhr对象
2. 调用xhr.open()
3. 设置Content-Type（内容格式、内容类型）
   - xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded')
4. 调用xhr.send(数据)
   - 数据为url编码格式
5. 设置readystatechange事件获取响应内容

## get与post发送方式的区别

**请求参数的书写位置不同：**

​          get请求方式：在xhr.open()的url后面使用?连接

​          post请求：在xhr.send()中书写

**post请求需要设置Content-Type**

## 封装ajax函数

```
// 封装函数，用于将对象转换为url编码格式
    function urlencoded(obj) {
      var arr = []; // 声明数组用来保存结果
      // 遍历obj，获取所有属性
      for (var k in obj) {
        // k - 属性名 - 字符串类型
        // obj[k] - 属性值
        arr.push(k + '=' + obj[k]);
      }
      return arr.join('&');
    }
    // 封装用来发送ajax请求的函数
    //  参数：
    //    对象
    //      - type 请求方式
    //      - url 请求地址
    //      - data 请求参数
    //      - success 回调函数
    function ajax(options) {
      // 1 创建xhr对象
      var xhr = new XMLHttpRequest();
      // 2 设置请求的相关信息: 需要根据请求方式分别设置
      //   - 统一保存数据
      var data = urlencoded(options.data);
      //  2.1 将请求方式统一转换为大写(或小写)
      var type = options.type.toUpperCase();
      //  2.2 对请求方式进行检测
      if (type === 'GET') {
        xhr.open('GET', options.url + '?' + data);
        xhr.send();
      } else if (type === 'POST') {
        xhr.open('POST', options.url);
        xhr.setRequestHeader('Content-Type', 'application/x-www-form-urlencoded');
        xhr.send(data);
      }
      // 3 设置事件接收响应内容
      xhr.onreadystatechange = function () {
        // 3.1 检测
        if (xhr.readyState === 4 && xhr.status === 200) {
          // 3.2 将JSON格式的字符串转换为对象
          var res = JSON.parse(xhr.responseText);
          options.success(res);
        }
      };
    }


// 进行数据处理的函数
    function urlencoded(obj) {
      var arr = []; // 声明数组用来保存结果
      // 遍历obj，获取所有属性
      for (var k in obj) {
        // k - 属性名 - 字符串类型
        // obj[k] - 属性值
        arr.push(k + '=' + obj[k]);
      }
      return arr.join('&');
    }
```

# FormData的使用

作用：

​     可以快速处理表单的数据 

​     可以进行文件上传

注意点:

​     **发送FormData需要使用POST请求方式**

​     **不需要单独设置Content-Type**

使用方式

​     单独发送数据

   ````
  // 1 空FormData对象，添加数据后发送
      // 1.1 创建FormData对象
      var fd = new FormData(); // 空的FormData对象
      // 1.2 向fd中添加一些数据
      fd.append('name', 'jack');
      fd.append('age', 18);
  
      // 1.3 使用POST方法将fd发送到对应接口（此处的接口为formdata）
      //  - 无需设置之前post的content-type
      var xhr = new XMLHttpRequest();
      xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata');
      xhr.send(fd); // 将fd放入在send()参数中即可
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 200) {
          console.log(xhr.responseText);
        }
      };
   ````

处理表单数据

```
  <!-- 设置form标签，用来进行formdata操作 -->
    <form id="testForm">
      <!-- 如果要表单元素数据被请求发送，必须设置name -->
      <input type="text" name="username">
      <input type="password" name="password">
      <!-- 设置按钮，点击后，使用FormData处理表单数据 -->
      <button type="button" id="btn">ajax提交</button>
    </form>
  
  
  // 2 通过FormData对象管理表单元素，再发送(同时也可以添加数据)
      document.getElementById('btn').onclick = function () {
        // 2.1 创建FormData对象，传入DOM对象形式的form标签到参数中
        var testForm = document.getElementById('testForm');
        var fd = new FormData(testForm); // 空的FormData对象
  
        // 2.1.1 也可以在存在form的基础上，自己添加数据
        fd.append('name', 'rose');
        fd.append('age', 21);
  
        // 2.3 使用POST方法将fd发送到对应接口（此处的接口为formdata）
        //  - 无需设置之前post的content-type
        var xhr = new XMLHttpRequest();
        xhr.open('POST', 'http://www.liulongbin.top:3006/api/formdata');
        xhr.send(fd); // 将fd放入在send()参数中即可
        xhr.onreadystatechange = function () {
          if (xhr.readyState === 4 && xhr.status === 200) {
            console.log(xhr.responseText);
          }
        };
      }
```

文件上传

1 准备结构(文件域)

```
<input type="file">
```

2 检测用户是否选择了文件

  对DOM对象形式的input[type="file"]的**files**属性进行检测,如果内部存储了任意的一个值，就说明选取了文件，                           否则就是没选

3 使用FormData保存文件信息 使用fd.append()添加即可

4 通过ajax发送

5 响应处理，展示服务端获取到的图片

## jQuery使用FormData上传文件的注意点

必须设置两个属性

contentType: false 不指定内容类型

processData: false 不进行数据处理

# 上传进度条功能

- xhr.upload.onprogress 上传中实时触发事件
  - 事件对象e的属性
    - e.lengthComputable 文件长度使用可用
    - e.loaded 以上传大小
    - e.total 总大小
- xhr.upload.onload 上传完毕时触发事件

# jQuery的全局ajax处理器

作用：用来对页面中的ajax操作进行统一设置，简化操作

常见场景：加载资源的loading功能

ajaxStart() 任意请求开始时触发内部回调

```
$(document).ajaxStart(function () {
  // 代码...
});
```

ajaxStop() 任意请求结束后触发内部回调

```
$(document).ajaxStop(function () {
  // 代码...
});
```

# axios使用

axios.get()的使用

```
// axios.get('地址', {params: {数据。。。}}).then(成功时的处理函数);
// 示例：
 axios.get('http://www.liulongbin.top:3006/api/getbooks', {
      params: {
        id: 2
      }
    })
      .then(function (res) {
        // axios对响应的res部分进行了包装，之前jQuery中的res，相当于axios中的res.data
        //  - 刚开始使用时，可以使用以下操作
        res = res.data;
        console.log(res);
      }); 
```

axios.post()的使用

```
// axios.post('地址', {数据。。。}).then(成功时的处理函数)
    axios.post('http://www.liulongbin.top:3006/api/post', {
      name: 'jack',
      age: 18
    })
      .then(function (res) {
        console.log(res);
      });
```

axios()的使用  发送get和post的区别：

**设置请求参数的属性名不同**:get请求参数的属性名为params  post为data

get:

```
axios({
      method: 'GET',
      url: 'http://www.liulongbin.top:3006/api/get',
      params: {
        name: 'jack',
        age: 18
      }
    })
      .then(function (res) {
        console.log(res.data);
      });
```

post:

```
axios({
      method: 'POST',
      url: 'http://www.liulongbin.top:3006/api/post',
      data: {
        name: 'rose',
        age: 21
      }
    })
      .then(function (res) {
        console.log(res.data);
      });
```

# 跨域

## 同源策略

指的是两个地址的 **协议 域名 端口** 完全一样，这两个地址就是同源的，或者称为同源地址

发送跨域请求时，请求发送是成功的，响应也是成功的，只不过浏览器将响应的信息拦截了，我们无法操作。

## 跨域方式

- JSONP
  - 兼容性好，但是只支持GET
- CORS 
  - 兼容性不太好，但是支持GET、POST，并且是标准中提供的方式。

## JSONP的实现原理

实现原理：

- 同源策略不限制script标签对非同源地址进行请求
- 可以借助script标签进行JSONP实现

实现方式:

```javascript
 <!-- 
    使用JSONP进行请求处理
      步骤:
        1 准备一个处理函数
        2 通过script标签的src属性，进行接口的请求

- 因为同源策略不会限制script标签的功能
入请求参数
- callback 用来传递本地处理函数的函数名
- 其他参数随便写
束后，步骤1设置的处理函数会自动调用
- 可以在处理函数中对响应数据进行后续处理
-->
 <script>
    function fun(res) {
      console.log(res);
    }
  </script>
  <script src="http://ajax.frontend.itheima.net:3006/api/jsonp?callback=fun&name=jack"></script>
```

JSONP和JSON没有本质关联

**JSONP与ajax没有任何关联**

​        JSONP是使用script标签进行请求发送

​       ajax是通过浏览器提供的XMLHttpRequest对象发送

## jQuery发送JSONP请求的方式

jQuery使用的是$.ajax()方法进行JSONP操作

- **设置dataType属性为'jsonp'**

小说明：

​    可以从浏览器的network看到请求的类型为 script 

​    jQuery会将使用过的用于发送jsonp请求的script标签移除，打开页面也看不到

```
	$.ajax({
      type: 'GET',
      url: 'http://ajax.frontend.tmall.net:3006/api/jsonp',
      data: {
        name: 'jack',
        age: 18
      },
      /* 
      // 下面的两个属性作为了解即可，通常不会使用
      jsonp: 'xyz', // 将默认的请求参数名callback设置为其他名称
      jsonpCallback: 'abc', // 将处理函数名称设置为指定名称
      */
      dataType: 'jsonp', // 设置这句话后，jQuery就会使用JSONP的方式进行请求发送
      success: function (res) {
        console.log(res);
      }
    });
```

# 节流和防抖

## 防抖

进行重复操作时，设置时间间隔，以最后一次满足间隔的操作为准进行执行。

简单来说：**就是以满足间隔的最后一次为准**

通过定时器进行设置

## 节流和防抖的区别

防抖是当指定间隔时间内再次触发，使用新触发的操作再次重新记时

节流是在指定间隔时间内再次触发，新操作会被忽略。

# HTTP协议

HTTP 协议即**超文本传输协议** (HyperText Transfer Protocol) ，它规定了**客户端与服务器之间进行网页内容传输时，所必须遵守的传输格式**。

## HTTP的请求报文和响应报文

内容传输格式分为**请求报文**和**响应报文**两种

请求报文（客户端给服务端发送请求时发送的那些内容）

**请求报文由4部分组成**

1.**请求行**:     3部分组成：  请求方式  请求地址  协议和版本

2.**请求头**：**用来保存客户端的相关信息**(大部分是浏览器自动设置的)

​                   Host：主机地址        User-Agent：用户代理字符串，客户端的一些浏览器和系统信息

​                  Content-Type：发送的请求体的内容类型(内容格式)

3.空行

4.**请求体**：**就是我们发送的请求参数**

​                  **get请求的参数在url中发送，请求体为空**

​                  **post请求的参数在请求体中**，所以需要设置Content-Type

响应报文由4部分组成

1.**状态行**:    由3部分组成： 协议和版本  状态码  状态文本

2.**响应头**：用来**保存服务端的相关信息**(有的是服务端自动设置的，有的是后端自己设置的)

​                  Content-Type: 响应体的内容类型

3.空行

4.**响应体**:**服务端发送给客户端的响应内容**（无论什么请求方式，响应的数据都在响应体中保存）

​                例如我们在jQuery中接收的res就是响应体

## 请求方式

最常用的是GET和POST

- GET 用来获取数据（查询）
- POST 用来发送数据（新增）
- PUT 用来修改数据（修改）
- DELETE  用来删除数据（删除）

## 状态码

**2xx 成功**，常见的是200

**3xx 重定向**(我们请求a.html，服务端认为a.html有问题，没法给你看，将你的请求转给了b.html)

​                    常见：304 读取缓存的内容了

**4xx 客户端错误**，常见的是404

**5xx 服务器错误**，通常为服务端有问题时出现