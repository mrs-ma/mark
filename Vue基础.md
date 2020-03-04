# Vue

## 获得vue

最新稳定版本：2.6.11

1) 直接下载

- 开发版本：<https://cdn.jsdelivr.net/npm/vue/dist/vue.js>
- 生产版本：<https://cdn.jsdelivr.net/npm/vue>

2) CDN(Content Delivery Network内容分布式部署)

<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

3) 使用 `npm`下载

npm install vue

## MVVM设计模式

mvvm设计模式可以解读为如下：

m: model  数据部分  data

v：view  视图部分  div容器

vm： view & model 视图和数据 的 结合体  

## vue指令

### 插值表达式

vue中如果需要在html标签的“**内容区域**”中表现数据，就可以使用**{{}}双花括号**，这个技术称为**插值表达式**

<标签> {{ 表达式 }} </标签>    表达式：变量、常量、算术运算符、比较运算符、逻辑运算符、三元运算符等等

### v-text

v-text与{{}}的作用是一样的，都是操控 标签的**内容区域**信息

<标签 v-text="表达式"> </标签>  v-text 是通过标签的**属性**形式呈现如果 标签 内容区域 有默认信息，则会被v-text                     覆盖掉v-text                                       可以进行 变量、常量、算术符号、比较符号、逻辑符号、三元运算符号等运算

### v-html

v-html 与 v-text、{{ }} 的作用一样，都是操控 标签的**内容区域**

<标签 v-html="表达式"> </标签>    v-html对 **html标签** 和 **普通文本** 内容都可以设置显示  标签的默认内容会被v-         html覆盖

###  属性绑定-简单使用

  {{ }}、v-text、v-html可以对标签的**内容区域**进行操作，操作标签的**属性**需要通过 v-bind: 指令

```
<标签 v-bind:属性名称="表达式" ></标签>
<标签 :属性名称="表达式"></标签>  // 简易方式设置，推荐使用              
```

 属性绑定-class属性

```
1) 对象方式
	<tag :class="{xx:true, xx:false}"></tag>
	<!--true: 设置   false:不设置-->

2) 数组方式
	<tag :class="['xx','yy','zz']"></tag>
	<!--数组元素值如果不是data成员 就要通过单引号圈选，代表是普通字符串-->
```

属性绑定-style属性

```
1) 对象方式    <tag :style="{xx:yy,xx:yy.....}"></tag>    <!--xx:样式名称，yy:样式的值-->
2) 数组方式    <tag :style="[{xx:yy},{xx:yy.....}]"></tag>    <!--根据需要，数组的每个元素都是一个对象，每个对象包含一对或多对css样式-->
```

### v-on(@)

在vue中给元素进行**事件**绑定，需要通过v-on:指令实现，也使用@符号，@是v-on:的简写，使用更方便

<tag @事件类型="事件处理驱动"></tag>   事件处理驱动 需要通过methods定义

vue“单击”事件参数的3种类型：

1. 有声明()，也有传递实参，形参就代表被传递的实参
2. 有声明(),但是没有传递实参，形参就是**undefined**
3. 没有声明()，第一个形参就是**事件对象**

### 事件绑定-this是谁

在Vue实例内部包括不限于methods方法中，**this关键字** 是Vue实例化对象，具体与 **new Vue()** 是一样的

并且其可以对 **data** 和 **methods**成员进行直接访问

### v-model**

在Vue中有一个很重要的指令，名称为v-model，其被称为**双向数据绑定**指令，就是Vue实例对数据进行修改，页面会立即感知，相反页面对数据进行修改，Vue内部也会立即感知

v-model是vue中**唯一**的双向数据绑定指令

v-model只针对**value属性**可以绑定，因此经常用在form表单标签中，例如input(输入框、单选按钮、复选框)/select(下拉列表)/textarea(文本域)，相反div、p标签不能用

v-model只能绑定**data成员**，不能设置其他表达式，否则错误

### v-for

```
<标签 v-for="成员值 in 数组"></标签>
<标签 v-for="(成员值,下标) in 数组"></标签>
```

:key介入   v-for使用的同时必须使用:key，以便vue能<font color=red>准确跟踪</font>每个节点，从而重用和重新排序现有元素，你需要为每个数据项提供一个唯一的、代表当前项目的属性值赋予给key

```
<标签 v-for="" :key="可以代表每个项目的唯一的值"></标签>
```

### v-if&v-show

在vue中，v-if 和 v-show 会根据接收  **true/false**  信息使得页面上元素达到<font color=red>显示</font>或<font color=red>隐藏</font>的效果

```
<标签 v-if="true/false"></标签>
<标签 v-show="true/false"></标签>
<!--true:显示   false:隐藏-->
```

v-if：通过 **创建**、**销毁** 方式达到显示、隐藏效果的(销毁后有一个占位符)

v-show：其是通过css控制达成显示、隐藏效果的

v-if 有更高的**切换消耗** 、v-show有更高的**渲染消耗**

如果需要**频繁**切换 则v-show 较合适，如果运行条件不大可能改变 则v-if 较合适。

### v-if&v-else

```
<标签 v-if="true/false"></标签>
<标签 v-else-if="true/false"></标签>
<标签 v-else-if="true/false"></标签>
<标签 v-else></标签>
```

# computed计算属性应用**

Vue本身支持模板中使用**复杂表达式**表现业务数据，但是这会使得模板内容过于杂乱，如果确有需求，可以通过computed计算属性实现，该computed可以对其他data做复杂合成处理的

在Vue实例内部创建计算属性(与el、data、methods并列位置处)，每个计算属性都需要通过**return**关键字返回处理结果

```
new Vue({
  el:xx,
  data:xx,
  computed:{
    // 属性名称:function(){
    属性名称(){
      // 业务表达式实现，可以通过this操作data成员
      return  返回结果
    }
  }
})
```

# 过滤器

在项目应用中，同样一份数据信息，表现形式确有千差万别，例如**时间信息**可以是对象、时间戳、格式化等，**字符 串**可以是大写的、小写的、首字母大写的等等，如果**提供方**给我们提供的信息是其中一种形式，而我们需要的是**另一种**，在Vue中，可以通过 “**过滤器**” 转换处理。过滤器是Vue中实现数据格式**转换**的一种机制。本质就是函数

Vue实例化过程中，与el、data平行的位置声明`filters`成员并在其中制作过滤器，这个过滤器只能被当前Vue实例使用，称为 "私有过滤器"

```
new Vue({
  filters:{
    // 如下方法格式是es6简易设置方式，完整写法： 过滤器名称:function(被处理数据){]}
    过滤器名称(被处理的数据){
      // 对数据进行加工处理
      return 结果
    },
    ...
  }
})
```

{{ 时间信息成员 | 过滤器名称 }}   模板中

**注**：过滤器只可以用在**两个**地方： <font color=red>插值表达式</font>和 <font color=red>:冒号 属性绑定表达式</font>。

​        过滤器不让使用this关键字，或者this关键字不是“Vue实例”

# 按键修饰符

​	`@keyup.ctrl.enter="XXX"`  表示 ctrl和enter一并触碰，才触发事件执行

# 自定义指令

获得焦点-私有

```
  // 注册自定义指令
      directives:{
        // 指令名称:{配置对象成员}
        // 指令名称注册时不要设置"v-",使用时再设置
        'dian':{
          // inserted是固定用法
          // inserted：时机的事情，代表是div容器被Vue实例编译完毕，并且也渲染好了
          inserted:function(m){
            // m：代表使用该指令的元素dom对象
            // dom对象可以通过webapi技术操作页面元素
            // m.style.color = 'red'
            m.focus() // 使得input框元素获得焦点
          }
        }
      },
```

# 扩展

## template

在Vue实例内部可以声明template，其内容可以**覆盖掉**原生的div容器的

## $mount

如果Vue没有提供`el`成员帮助找到div容器，那么可以调用$mount()方法

因此Vue实例与容器联系有两种方式：

1) el:'#app'

2) $mount方式

## render成员

在Vue中如果定义了render成员，那么其提供的内容会渲染到页面中，并且会**覆盖**原容器，包括template

优先级关系：render >>>>> template >>>>>>默认容器

## console使用

console.dir()   可以把dom对象的各个成员给打印出来

console.group()  对输出的信息做分组处理，更加清楚

console.log('%c%s',css样式设置, 被输出的信息)

## 生命周期

生命周期是指vue实例(或者组件)从诞生到消亡所经历的各个阶段的总和

生命周期分为3个阶段，分别是[创建]()、[运行]()、[销毁]()

- 创建阶段：由空白期、data/methods初始化、模板挂载、模板渲染等组成
- 运行阶段：分为 更新前 和 更新后 两部分
- 销毁阶段：分为 销毁前 和 销毁后

​	创建：beforeCreate    **created**   beforeMount   mounted

​	运行：beforeUpdate  updated

​	销毁:  beforeDestroy    destroyed

beforeCreate：此时Vue对象刚创建好，没有任何成员，data、methods等都没有呢，只有this

**created**：此时vue对象已经长大一点，内部已经完成了data、methods等成员的设置，也是data初始化的最好时机

beforeMount：此时vue实例已经把div容器给获得到了，但是内部的vue指令等信息还没有被编译处理

mounted：此时，vue获取到的div容器内部的原生指令已经被编译处理好了，并且也完成了容器的渲染工作，此时模板中已经看不到vue原始指令了

# Promise

 Promise，它是一个对象，是用来处理**异步**操作的，可以让我们写异步调用的代码更加优雅、美观、有利于阅读。

`Promise的三种状态`：

1. pending（进行中）

2. resolved（完成）

3. rejected（失败） 

   

   ```
   // 1. 创建Promise对象
   var p = new Promise(function(resole,reject){
     if(异步操作成功){
     	resole(res)
     }else{
       reject(cuo)
     }
   })
   
   // 2. 对Promise对象结果进行处理
   p
     .then(
     	function(data){
       	// data 与 res一致，代表成功输出结果
     	}
   	)
     .catch(
     	function(err){
         // err 与 cuo一致，代表失败输出结果
       }
   	)
   ```

   resolve: 异步操作成功的回调函数

   reject：异步操作失败的回调函数

   # axios

   axios是对**ajax封装**的一个产品

​       axios获取3种方式：

1.   直接下载源文件  推荐

2.   通过script标签引入，需要上网环境

3.   npm  install axios  

    axios.defaults.baseURL = 公共根地址

   在Vue的大环境中不要直接使用axios，相反要把其配置成为Vue的成员，通过Vue对象调用

   // 原型继承成员名称为 $http ，也可以配置为其他名称
   Vue.prototype.$http = axios

   # 拦截器-interceptors

   拦截器是axios向服务器端发送**请求**和**响应**回来所经历的两道关口

   axios本身有两种拦截器：[请求拦截]()、响应拦截

   ```
   // 请求拦截器
   axios.interceptors.request.use(function (config) {
     // 放置业务逻辑代码
     return config;
   }, function (error) {
     // axios发生错误的处理
     return Promise.reject(error);
   });
   ```

   ```
   // 响应拦截器
   axios.interceptors.response.use(function (response) {
     // 放置业务逻辑代码
     // response是服务器端返回来的数据信息，与Promise获得数据一致
     return response;
   }, function (error) {
     // axios请求服务器端发生错误的处理
     return Promise.reject(error);
   });
   ```

   