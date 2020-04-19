# ES6

## ES6 是什么

[ECMAScript](https://baike.baidu.com/item/ECMAScript/1889420) 6，简称ES6 。是 Javascript 语言下一代标准。随着js语言应用场景的不断扩展，开发者需要编写的代码越来越复杂。在这个背景下，ES6 的目标是`使JavaScript语言可以用来编写复杂的大型应用程序，成为企业级开发语言 `。ES 是一种语言标准，6表示版本号。

ES2015：称为es6。

**ES6有两层含义**

特指ECMAScript2015

泛指ES2015及之后的新增特性，虽然之后的版本应当称为ES2018，ES2019...但可统称为ES6。

ES6新增了很多强大的语法，如下是比较常使用的：

1. let 和 const
2. 解构赋值
3. 函数扩展
4. 字符串扩展
5. 数组扩展
6. 对象的简写

## let 和 const

### let 变量

作用：定义变量。（var也是用来定义变量）

与var的区别:

- 不能重复定义
- 没有变量提升（var定义的变量是有变量提升的），必须`先定义再使用`
- 全局变量不会附加到window对象的属性中
- 具有块级作用域

### const 常量

作用：定义一个只读的常量。

区别于变量名，常量名**推荐采用全大写**的方式，多个单词之间**使用_下划线分隔**

所谓常量，就是不能修改，即：

- 一旦定义就不能修改；
- 一旦声明，就必须立即初始化；
- 其它与let相似的特点

  - 具有块级作用域
  - 没有变量提升，必须先定义再使用
  - 常量也是独立的，定义后不会添加为window对象的属性

对于复杂类型数据（如对象和数组），变量指向的内存单元，保存的只是一个指向实际数据的指针，`const`只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它指向的数据结构是不是可变的，就不能控制了。因此，`将一个对象声明为常量必须非常小心,它的属性是可以修改的`。

如果你真的希望**定义一个不能修改的对象**（属性不能添加，修改，删除），你可以使用Object.freeze()。下面是一段参考代码：它一个可以把一个对象全部冻结的函数（深冻结）:

```
// 设置函数，对一个对象进行深冻结(用于防止复杂数据被修改)
function deepFreeze(obj) {
  Object.freeze(obj);
  for (var k in obj) {
    if (typeof obj[k] === 'object') {
      deepFreeze(obj[k]);
    }
  }
}

// 声明要冻结的对象
const obj = {
  name: 'jack',
  age: 18,
  hobbies: {
    eat: '吃',
    drink: '喝',
    run: '跑步',
    playBall: ['篮球', '弹球', '悠悠球']
  }
};

// 调用函数冻结对象obj
deepFreeze(obj);
obj.name = 'rose';
obj.hobbies.eat = '各种吃';
obj.hobbies.playBall[2] = '各种弹';
console.log(obj); // obj没有变化，说明冻结完成
```

## 解构赋值

### 定义

ES6 允许按照一定**模式**，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。

### 数组的解构赋值

它能够快速从数组中取出值保存到变量中。它的本质是给变量赋值

格式：

```
let [变量1=默认值1, 变量2=默认值2, 变量n=默认值n] = [数组元素1, 数组元素2, 数组元素n];
```

规则：

- 赋值符号左右两边都是数组，把右边的数组按下标从小到大取出来，放入左边的数组中。
- 如果左边的变量并没有分配到某一个值：
  - 有默认值，使用其默认值。
  - 无默认值，其值是undefined
- 最开始的let可选，也可写成var或省略，与解构赋值功能无关，仅代表变量的声明方式。

```
// 1 变量多，值少:
let arr = [5, 9, 10];
let [a, b, c, d] = arr;
console.log(a, b, c, d); // 5 9 10 undefined
// 结论：没有匹配上的值是undefined

// 2 默认值:
let arr = [5, 9];
let [a, b, c, d = 4] = arr;
console.log(a, b, c, d); // 5 9 undefined 4
// 结论：对于没有匹配上的变量，有默认值就使用默认值，否则就是 undefined，

// 3 变量少，值多:
let arr = [5, 9, 10, 8, 3, 2];
let [a, b] = arr;
console.log(a, b); // 5 9
// 结论：多余的忽略

// 4 用空跳过不需要的值:
let arr = [5, 9, 10, 8, 3, 2];
let [, , a, , b] = arr; 
console.log(a, b); // 10 3
// 结论：不需要用变量接收的值，用空位占位

// 5 复杂的场景，只要符合模式，即可解构:
let arr = ['zhangsan', 18, ['175cm', '65kg']];
// 5.1 如何让a的值是175cm,b的值是65kg?
let [, , [a, b]] = arr;
console.log(a, b); // '175cm' '65kg'
// 5.2 如何让wxyz对应arr中的四个数据呢？
let [w, x, [y, z]] = arr;
console.log(w, x, y, z); // 'zhangsan' 18 '175cm' '65kg'
```

剩余值

```
let arr = [5, 9, 10, 8, 3, 2];
let [a, b, ...c] = arr; // ...c 接收剩余的其他值，得到的c是一个数组
console.log(a, b, c); // 结果为： 5 9 [10, 8, 3, 2]
```

注意：

- ... **只能用在最后一个变量上**。这个变量一定是一个数组。
- 在解构赋值的过程中，如果有出现数组元素个数大于变量个数的情况，它将会把多余的参数起来，保存在这个数组。如果元素个数不足（没有剩余元素），也会返回空数组。

### 对象的解构赋值

作用：快速从对象中获取值保存到变量中。它的本质是给变量赋值。

完整格式:

```
let {"属性名1"：变量名1=默认值1, "属性名2"：变量名2=默认值2,... } = {"属性名1"：属性值1,"属性名2"：属性值2,...}
```

解析规则：

- 默认值是可选的。你可以指定默认值，也可以不指定。
- 右边的"属性名"与左边的“属性名” 一致，则把右边的属性值赋值给左边的变量名。
- 如果右边的匹配不成立，看看是否有使用默认值，有默认值就使用默认值，没有就是undefined。

如果左侧对象中属性名与变量名相同，则可左侧合并：

```
let {变量名1=默认值1，变量名2=默认值2} = {"属性名1"：属性值1,"属性名2"：属性值2,...}
```

场景1，变量名和属性名一样

```
// 场景1，默认要求变量名和属性名一样
let { name, age } = {age: 27, name: 'jack'};
console.log(name, age); // 'jack' 27

let {a, c} = {a: 'hello', b: 'world'};
console.log(a, c); // 'hello' undefined
```

场景2，变量改名

```
// 场景2，可以通过:为变量改名
let {b, name:a} = {name: '李雷'};
console.log(b, a, name); // undefined '李雷' undefined
// 解释：操作中，将属性name的值保存给变量a，所以只有a有值
```

```
// 默认值:
var {b=1, name:a,age:b=20 } = {name: '韩梅梅'};
console.log(b, a, name); // 20 '韩梅梅' undefined


// 复杂的嵌套，只要符合模式，即可解构
let obj = {
    name: '小红',
    age: 22,
    dog: {
        name: '小明',
        gender: '男'
    }
};
// 如何才能把age和name解析出来
let {name, age, dog: {name：dogName, gender}} = obj;
console.log(name, age, dogName, gender); // '小红' 22 '小明' '男'


// 假设从服务器上获取的数据如下
let response = {
    data: ['a', 'b', 'c'],
    meta: {
        code: 200,
        msg: '获取数据成功'
    }
}
// 如何获取到 code 和 msg
let { meta: { code, msg } } = response;
console.log(code, msg); // 200 '获取数据成功'


let {max,min,PI} = Math;
```

剩余值

```
// 把其它的属性全收集起来
let obj = {name:'zs', age:20, gender:'男'};
let {name, ...a} = obj;
console.log(name, a);
// 结果：
// name = zs
// a = {age: 20, gender: "男"};
```

## 定义对象的简洁方式

```
let name = 'zhangsan', age = 20, gender = '女';
let obj = {
    name: name, // 原来的写法
    age, // 对象属性和变量名相同，可以省略后面的 “:age”，下面的gender同理
    gender,
    fn1 : function(){  // 常规写法
        console.log(123);
    },
    fn2 () { // function可以省略 
        console.log(456);
    }
};
console.log(obj.age); // 20
obj.fn2(); // 456
```

## 函数的拓展

### 参数默认值

在定义一个函数时，我们可以给形参设置默认值：当用户不传入对应实参时，我们有一个保底的值可以使用。这个特性在ES6之前，是不支持的，我们以前会通过一些变通的方式来实现。

传统：

```
// ES5 中给参数设置默认值的变通做法，以ajax函数部分封装为示例：
function ajax (type, url, isAsync) {
	// 基本写法：  
  if(isAsync === undefined){
      isAsync = true;
  }
  // 简化写法：
	// isAsync = isAsync || true;
  
  console.log(type, url, isAsync);
	//.. 其他代码略
}
// 下面这两句是等价的
open("get","common/get"); // 参数3使用默认值true
open("get","common/get",true);

open("get","common/get",false);
```

es6：

```
function open(type, url, isAsync = true) {
    console.log(type, url, isAsync);
}
// 下面这两句是等价的
open("get","common/get")；// // 参数3使用默认值true
open("get","common/get",true);

open("get","common/get",false); 
```

rest 参数:rest （其它的，剩余的）参数 用于获取函数多余参数，把它们放在一个数组中。

在定义函数时，在最后一个参数前面加上`...`， 则这个参数就是剩余参数；

问题：编写一个函数，求所有参数之和；

方法一：arguments

```
function getSum (){
    //  在这里写你的代码
    var sum = 0 ; 
    for(var i = 0; i < arguments.length; i++){
        console.info( arguemnts[i])
        sum += arguments[i];
    }
}
```

方法二：rest参数

```
// 参数很多，不确定多少个，可以使用剩余参数
const  getSum = (...values) => {
    var sum = 0 ; 
    for(var i = 0; i < values.length; i++){
        console.info( values[i])
        sum += values[i];
    }
}
// 调用
console.log(fn(6, 1, 100, 9, 10));
```

与arguments相比，它是一个真正的数组，可以使用全部的数组的方法。

### 箭头函数

箭头函数本质上是 匿名函数的简化写法。

格式:

```
let 函数名 = (形参1，...形参n) => {
    // 函数体
};
```

1. 去除function关键字
2. 在形参和函数体之间设置 `=>`

当形参有且只有一个，可以省略小括号

当函数体只有一条语句，可以省略大括号; 

当函数体只有一条语句，并且就是return语句，则可以省略return和大括号。

注意如果返回值是一个对象，要加()

```
let f = x => { return {a:1};  }
// 可以简化成：
let f = x => {a:1}; // 如果不加，{}会被认为是函数的代码块，不会被解析器当成对象处理
let f = x => ({a:1});
```

箭头函数与普通函数的区别:

- 内部没有this
- 内部没有arguments（了解）
- 不能作为构造器（了解）

内部的`this`对象，指向定义时所在的对象，而不是使用时所在的对象。

```
// 箭头函数中this的问题：
let obj = {
  name: 'jack',
  age: 18,
  sayHi() {
    // 方法中直接访问this：
    console.log(this); // 对象obj

    // 普通调用的函数中的this：
    var f1 = () => {
      console.log(this); // 对象obj
    };
    f1();

    // 同上：
    setTimeout(() => {
      console.log(this); // 对象obj
    }, 0);

    // 另一个对象的方法中的this
    let obj2 = { name: 'rose' };
    obj2.sayHehe = () => {
      console.log(this); // 对象obj
    };
    obj2.sayHaha = function () {
      console.log(this); // 对象obj2，因为没有使用箭头函数
    };
    obj2.sayHehe();
    obj2.sayHaha();

  }
};
obj.sayHi();
```

## 数组的扩展

### 扩展运算符

功能：它的作用是把数组中的元素一项项地展开：把一个整体的数组拆开成单个的元素。

格式：`...数组`

```
console.log(...[1,2,3]);
```

 数组合并

```
var arr0 = ['a', 'b'];
var arr1 = [1, 2, 3];
var arr2 = [...arr1];
var arr3 = [...arr0, ...arr1];
```

### Array.from()

功能：把其它伪数组的对象转成数组。

### find方法

```
let result = [].find(function(item,index,self){ 
    //...
    // 如果满足查找的条件
    return true;
});
- 回调函数有三个参数，分别表示：数组元素的值、索引及整个数组
- 如果某次循环返回的是true，find和findIndex方法的返回值就是满足这个条件的第一个元素或索引
- 如果在回调函数体内，某个时刻return true，则表示查找过程结果，返回值就是本轮循环中的元素（或者是下标）；如果全部的循环结束，也没有return true，则表示没有找到，没有找到会返回undefined。
- findIndex 找到数组中第一个满足条件的成员并返回该成员的索引，如果找不到返回 -1。

```

### includes()

断数组是否包含某个值，返回 true / false

- 参数1，必须，表示查找的内容
- 参数2，可选，表示开始查找的位置，0表示从第一个元素开始找。默认值是0。

## Set对象

Set是集合的意思。是ES6 中新增的内置对象，它类似于数组，但是`成员的值都是唯一的，即没有重复的值`。使用它可以方便地实现用它就可以实现数组去重的操作。

```
// 1. 基本使用
let set = new Set();
// 得到一个空的Set对象

let set = new Set([1,2,3])
```

### Set 的成员方法

- `size`：属性，获取 `set` 中成员的个数，相当于数组中的 `length`
- `add(value)`：添加某个值，返回 Set 结构本身。
- `delete(value)`：删除某个值，返回一个布尔值，表示删除是否成功。
- `has(value)`：返回一个布尔值，表示该值是否为`Set`的成员。
- `clear()`：清除所有成员，没有返回值。
- ` forEach`:遍历

### 应用-数组去重

```
let arr = [1,1,2,3,3];
console.log([...new Set(arr)])
```

## String的扩展

### 模板字符串

在做字符串拼接时，使用`+`来拼接复杂内容是很麻烦的，而模板字符串可以解决这个问题。

格式：\``${变量}` `${表达式}`\`

语法：

- 模板字 符串使用反引号 **`** 把内容括起来，类似于普通字符串的""。
- ${}充当界定符的作用，其中可以写变量名，表达式等。
- 允许字符串内部进行换行，代码更好读更好的体验

示例：

```
let name = 'zs';
let age = 18;
// 拼接多个变量，在模板字符串中使用占位的方式，更易懂
let str = `我是${name}，今年${age}`;

// 内容过多可以直接换行
let obj = [{name: 'flex', age: 20},{name: 'james', age: 21}];

let arr = ['175cm', '60kg'];
let html = `
	<div>
		<ul>
			<li>${obj.name}</li>
			<li>${obj.age}</li>
			<li>${arr[0]}</li>
			<li>${arr[1]}</li>
		</ul>
	</div>`;
```

### includes()

格式：`str.includes(searchString, [position])`	

功能：返回布尔值，表示是否找到了参数字符串

- position: 从当前字符串的哪个索引位置开始搜寻子字符串，默认值为0。

### startsWith()

- 格式：`str.startsWidth(searchString, [position])`         
- 功能：返回布尔值，表示参数字符串是否在原字符串的头部或指定位置
  - position: 在 `str` 中搜索 `searchString` 的开始位置，默认值为 0，也就是真正的字符串开头处。

### endsWith()

- 格式：`str.endsWith(searchString, [len])`            
- 功能：返回布尔值，表示参数字符串是否在原字符串的尾部或指定位置.
  - len:可选。作为 `str` 的长度。默认值为 `str.length`。

### repeat()

`repeat`方法返回一个新字符串，表示将原字符串重复`n`次。

语法:`str.repeat(n)`

```
let html = '<li>league</li>';
html = html.repeat(10);
```

## ES 6 降级处理

因为 ES 6 有浏览器兼容性问题，可以使用一些工具进行降级（把ES6的代码转成ES5的代码·），例如：**babel**