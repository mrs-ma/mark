# app分类

app就是运行在移动设备上的程序；

按开发方式分类：

- 原生开发     （安卓，ios）
- web开发（网页）
- 混合开发

# 访问网页时，服务器是如何知道当前用户是pc还是手机？

从客户端浏览器向服务器发请求时，会自动携带请求头，后端是可以收到这个请求头的。

其中有一个头叫：`User-agent`(用户代理)。它保存的字符串就可以用来识别当前的浏览器的信息。

服务器收到不同的头，会分析，决定是否要跳转到pc，或者是移动端。

如果要跳转，就给302状态码，并设置location响应头，则浏览器会自动跳转

# webApp

就是一个移动端的网站。

# HybridApp 混合模式

在html5页面的之外，包一个原生的壳webView。

# 三种跨平台的开发方式

跨平台：我只写一次代码，就可以生成ios，安卓的app。

技术：

- RN:react native
- weex
- flutter

# 多端开发

目标:写一次代码，运行在不同的**端**（微信小程序，百度小程序，头条小程序.....）

代表：

- taro: JD. 基于react。 
- uni-app: ucloud,基于vue

# hbuilder x 和mui

- hbuilder x:编辑器（不止于编辑器）
- mui: 它是一套移动端ui框架。它与hbuilder无缝配合，有大量快捷键和完备ui文档

# 连接手机模拟器，启动5+plus功能

必须在真机或者是模拟器中才会运行。

```
document.addEventListener('plusready',()=>{
	// plus 对象就是一切原生能力的来源。
    // 它会挂到window对象
})
```

# 打包app

- 配置manifest.json。
  - 地图要申请密钥。
- 云打包。
- apk传到手机中，安装.

# 如何打包已有的h5项目

​     去配置manifest.json文件

- - 在hbuilder中配置好了，再拷贝到vue项目的public目录下
- vue正常打包，所有的文件会在dist目录下
- 在hbuilder中打开dist目录，由于它有manifest.json文件，则它会自动识别为5+runtime项目
- 正常打包
- 把安装包下载下来，安装在手机上。

# Object.defineProperty()

作用：**定义**或者是**修改**对象的属性。

configurable: 能否再次修改

enumerable：能否枚举

value:设置初始值；

writable：是否可以修改这个属性值

```
Object.defineProperty(obj,"age",{
    // get:function(){

    // },
    get(){
        // 当你去访问age属性时，它就会自动执行；
        // 这个函数的返回值，就表示当前属性的值。
        console.log("获取age")
        // return Date.now()
        return _age;
    },
    set(val){
        // 当我们设置这个属性时，它就会执行
        // 它会接收一个参数，就是当前要设置给这个属性的值
        console.log("设置age为",val)
        _age = val
    }
})

```

get和set它们与value和writable是互斥的

# proxy

 Proxy（es6） 将在vue3版本中，用来实现数据响应式
 Proxy:代理。它是一个构造器。
 功能：通过Proxy创建对象，所创建的对象称为代理对象。

```
// Object.defineProperty() 在vue2.X版本中，用来实现数据响应式
// Proxy（es6） 将在vue3版本中，用来实现数据响应式
// Proxy:代理。它是一个构造器。
// 功能：通过Proxy创建对象，所创建的对象称为代理对象。
// 格式：
// var newObj = new Proxy(原对象,{代理列表})

let obj = {
    a: 1,
    age:30
}
var newObj = new Proxy(obj,{
    // target就是当前代理的那个原对象obj
    // key就是当前要访问的属性
    // receiver就是代理对象 newObj
    get(target,key,receiver){
        // 当访问对象的属性就会进入get函数
        console.log( target,key,receiver )
        return obj[key]
    },
    // value就是当前要设置的值
    set(target,key,value){
        // 当访问对象的属性就会进入set函数
        console.log( target,key,value )
    },
})
newObj.age = 20
```

# 面试题：创建一个允许负数做下标的数组

```
<script type="text/javascript">
    // 创建一个允许负数做下标的数组
    var arr = [1,2,3,5,6];

// console.log(arr[1]);
// var arr1 = new Proxy(原对象,{代理列表})
var arr1 = new Proxy(arr,{
    get(target,key){
        console.log( "获取" )
        // console.log( target,key)
        if(key > arr.length-1){
            // 数组越界
            console.error("智能提示，你的数组下标越界了",key)
            return undefined
        }
        if(key>=0) {

            return arr[key]
        } else {
            let newIndex = arr.length + key*1
            console.log( '获取的下标是负数:',key,newIndex)
            // return 
            return arr[newIndex]
        }
    },
    set(target,key,value){
        console.log( "设置" )
        console.log( target,key,value )
        if(key >=0){
            arr[key] = value
        }else {
            let newIndex = arr.length + key*1
            console.log( '设置的下标是负数:',key,newIndex)
            arr[newIndex] = value
        }
    }
})
// var arr1 = []
// 目标：写一段代码，得到一个arr1,

// ....
// (1)让这个arr1支持负数做下标
// arr1[-1] 就是arr中倒数第1个元素 ==>3
// arr1[-2] 就是arr中倒数第2个元素 ==>
// (2) 当用户访问的下标超过最大长度，不要给出undefined
//     而是给出一个错误提示

// ....
// console.log(arr1[-1])

</script>
```

# mvvm与vuejs

## 实现mvvm构造器，拦截对data属性操作

```
<script type="text/javascript">
	// 创建一个观察者
	var ec = new EventCenter()		
    // 实现一个基本的构造器
    // 功能：
    //   对options中data的所有属性进行拦截
    function MVVM(options) {
    // let _data = options.data
    const {data} = options
    // console.log(options.data)
    // 通过Objecject.defineProperty来拦截对data属性的操作
    // 在构造器内部，this是一个对象，就指向的是当前实例
    // console.log(this === vm);
    // this.abc = "123"

    for(let key in data) {
        Object.defineProperty(this,key,{
            set(val){
                console.log(`${key} 设置${val}`)
                data[key] = val
                // 发布事件，则所有的观察者都应该去执行
			   ec.emit(key);
            },
            get() {
                console.log(`获取${key}`)
                return data[key]
            }
        })
    }
}
</script>
```

## 新添加一个解析构造器

```
// 用来对模板进行解析，分析出哪个dom中需要显示数据初值
// 哪些dom结点，当数据变化时，它们还要跟着更新
// el : 选择器 #app
// vm : 就是MVVM的实例
function Compiler(el,vm){
    //选出对应的dom结构 
    this.dom = document.querySelector(el)
    // console.log(this.dom);
    this.compile( this.dom)

}

Compiler.prototype.compile = function(dom){
    // 整体目标：遍历dom，依次找出所有的dom节点，对它们做两件事：
    // childNodes 会收集所有的子节点
    //   包括换行，空格.....
    dom.childNodes.forEach(node=> {
        // 根据不同的节点类型来处理
        // 文本节点的nodeType === 3. 它就是文本
        // 元素节点的nodeType === 1. 它是标签
        // console.log(node.nodeType, node)
        if(node.nodeType === 3) {
            this.compileText(node)
        } else if(node.nodeType === 1){
            this.compileElement(node)
            // 如果是元素结点，则还要进一步去解析
            this.compile(node)
        }
    })
    // - 解析显示值。找出{{message}}，赋值为1000。
    // - 成为观察者。当这个属性变化时，可以再次去更新。
    // console.log( dom )
}
Compiler.prototype.compileText = function(dom) {
    console.log( "解析文本节点",dom)
}
Compiler.prototype.compileElement = function(dom) {
    console.log( "解析元素节点",dom)
}
```

## 处理文本节点-显示数据

```
 Compiler.prototype.compileText = function(dom) {
     console.log( "解析文本节点",dom)
     // 解析显示值。找出{{message}}，赋值为1000。
     // todo 成为观察者。当这个属性变化时，可以再次去更新。

     // 1. 取出文本节点的内容 
     var str = dom.textContent
     // 2. 通过正则替换
     // 一定要使用 =>
     var newStr = str.replace(/{{(.+?)}}/g,(objstr,p1)=>{
         // console.log(this)
         // console.log(objstr,p1)
         return this.vm[p1]
     }) ;
     // console.log(this.vm)

     // 3. 显示替换的结果
     dom.textContent = newStr
 }
```

## 处理文本结点-从数据到视图

- 引入观察者
- 在拦截器的set中添加 `发布事件`
- 在编译器中添加 `监听者`

```
 arrkeys.forEach(key => {
				// 给事件中心添加事件   
				ec.addListener(key,()=>{
					console.log(`${key},变化了`)
					
					// 1. 取出文本节点的内容 str
				
					// 2. 通过正则替换
					// 一定要使用 =>
					var newStr = str.replace(/{{(.+?)}}/g,(objstr,p1)=>{
							
						return this.vm[p1]
					}) ;
					// 3. 显示替换的结果
					dom.textContent = newStr
				})
			   })
```



## 处理元素节点v-model-显示数据

```
Compiler.prototype.compileElement = function(dom) {
    console.log( "解析元素节点",dom)
    // 1. 检查是否有v-model属性
    console.dir(dom)，
    // 当前节点有v-model属性
    if( dom.hasAttribute("v-model") ) {
        // 取出属性值：
        var key = dom.getAttribute("v-model");
        console.log(key)

        // 把对象中的key属性的值，显示在当前的input框中。
        dom.value = this.vm[key]

    }
}
```

## 处理元素节点-从数据到视图

在编译器中添加 `监听者`

```
Compiler.prototype.compileElement = function(dom) {
    console.log( "解析元素节点",dom)
    // 1. 检查是否有v-model属性
    console.dir(dom)
    // 当前节点有v-model属性
    if( dom.hasAttribute("v-model") ) {
        // 取出属性值：
        var key = dom.getAttribute("v-model");
        console.log(key)

        // 把对象中的key属性的值，显示在当前的input框中。
        dom.value = this.vm[key]

        // 添加监听者
        // 当key属性发生变化时，去更新input框中的值
        ec.addListener(key,()=>{
            dom.value = this.vm[key]
        })

    }
}
```

## 给表单元素添加input事件，实现从视图到数据

```
// 当前节点有v-model属性
if( dom.hasAttribute("v-model") ) {
    // 取出属性值：
    // 把对象中的key属性的值，显示在当前的input框中。
    var key = dom.getAttribute("v-model");
    dom.value = this.vm[key]

    // 添加监听者
    // 当key属性发生变化时，去更新input框中的值
    ec.addListener(key,()=>{
        dom.value = this.vm[key]
    })

    // 给元素本身添加input事件
    dom.addEventListener("input",(e)=>{
        // console.dir(e)
        // 1. 获取当前用户改完之后的值
        console.log(e.target.value)
        // 2. 设置给对象的属性值（数据）
        //    会进入到set拦截器,发布消息
+        this.vm[key] = e.target.value

        console.log("用户在input中做了修改")
    })

}
```

# 服务器渲染

SSR : server side render 。

渲染是：数据（json） -----> html文档（dom ）  它是发生在服务器端的。

即：从服务器获取回来的直接就是整个页面（包含数据）

## nuxt.js

它是一个包，要额外安装。

它集成了vue,vue-router,vuex,webpack,babel,vue-ssr.........................

它不是vue官方的产品

它可以用vue开发服务器端渲染的单页应用

## asyncData

- asyncData是Nuxt中额外增加的 vue 生命周期的钩子函数。
- 在这个钩子函数中，代码是在**服务端执行**。
- 没有 Vue 实例的 this，this 指向 undefined
- 它获取数据，以**对象格式返回**，并最终会附加到**vue组件的data数据项**中。

## 生命周期

- 在服务器端要执行：
  - asyncData
  - **beforeCreate(在服务器和客户端都会执行)**
  - **created(在服务器和客户端都会执行)**
- 在客户端要执行
  - asyncData(在路由切换时，它也会执行)
  - **beforeCreate(在服务器和客户端都会执行)**
  - **created(在服务器和客户端都会执行)**
  - mounted