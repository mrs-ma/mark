# JavaScript面向对象

面向过程:面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次调用就可以了。

面向对象:面向对象是把事务分解成为一个个对象，然后由对象之间分工与合作。

面向对象三大特性:封装性 继承性  多态性

# ES6中的类和对象

ES5：没有类，ES6：类

类模拟抽象的，泛指的，对象是具体的

## 创建类

```
语法：class 类名 {属性和方法}【类就是构造函数语法糖】

class Person {}

注意类名首字母大写

类要抽取公共属性方法，定义一个类
```

## 类constructor构造函数

```
class Star {
	constructor (uname,age){
		this.uname = uname;
		this.age = age;
	}
}

属性：放到constructor，构造函数里面
注意：类里面的方法不带function，直接写既可
类里面要有属性方法，属性方法要是想放到类里面，我们用constructor构造器
构造函数作用：接收参数，返回实例对象，new的时候主动执行，主要放一些公共的属性
注意：每个类里面一定有构造函数，如果没有显示定义, 类内部会自动给我们创建一个constructor() ，
注意：this代表当前实力化对象，谁new就代表谁
```

## 类添加方法

语法：注意方法和方法之间不能加逗号

```

class Star {
	constructor () {}
	sing () {}
	tiao () {}
}
注意：类中定义属性，调用方法都得用this
this.属性
this.方法()
```

**总结：类有对象的公共属性和方法，用class创建，class里面包含constructor和方法，我们把公共属性放到constructor里面，把公共方法直接往后写既可，但是注意不要加逗号**

# 类的继承

## **extends**

```
语法：
​	class Father {}
​	class Son extends Father{}
注意：是子类继承父类
```

## **super关键字**

我们应用的过程中会遇到父类子类都有的属性，此时，没必要再写一次，可以直接调用父类的方法就可以了

super关键字用于访问和调用对象父类上的函数。可以调用父类的构造函数，也可以调用父类的普通函数

**调用父类构造函数**

```
class F { constructor(name, age){} }

class S extends F { constructor (name, age) { super(name,age); } }

注意: 子类在构造函数中使用super, 必须放到this 前面(必须先调用父类的构造方法,在使用子类构造方法
```

**调用父类普通函数**

```
class F { constructor(name, age){} say () {} }

class S extends F { constructor (name, age) { super(name,age); } say () { super.say() } }

注意：如果子类也有相同的方法，优先指向子类，就近原则
```

属性和方法：

​	属性：如果子类既想有自己的属性，又想继承父类的属性，那么我们用super【super(参数，参数)】

​	方法：如果子类和父类有相同的方法，加入子类依旧想用父类的方法，那么我们用super调用【super.方法()】

如果子类不写东西，那么直接继承父类就可以用 

但是如果子类有自己的构造函数和父类同名的方法，此时不可以直接用父类的东西，需要用super调用父类的方法和构造函数

# 构造函数和原型

## 构造函数和原型

ES6，全称ECMAScript6.0 ，2015.06 发版。但是目前浏览器的JavaScript 是ES5 版本，大多数高版本的浏览器也支持ES6，不过只实现了ES6 的部分特性和功能。

在ES6之前，对象不是基于类创建的，而是用一种称为构建函数的特殊函数来定义对象和它们的特征。

构造函数是一种特殊的函数，主要用来初始化对象，即为对象成员变量赋初始值，它总与new一起使用。我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个函数里面。
function Fn () {}

## 创建对象可以通过以下三种方式

- 对象字面量
- new Object()【构造函数】
- 自定义构造函数

## **new在执行时会做四件事情**

1. 在内存中创建一个新的空对象。
2. 让this指向这个新的对象。
3. 执行构造函数里面的代码，给这个新对象添加属性和方法。
4. 返回这个新对象（所以构造函数里面不需要return）。

# 静态成员和实例成员

静态成员：在构造函数本上添加的成员称为静态成员，只能由构造函数本身来访问

实例成员：在构造函数内部创建的对象成员称为实例成员，只能由实例化的对象来访问

# 构造函数原型prototype

当实例化对象的时候，属性好理解，属性名属性值，那么方法是函数，函数是复杂数据类型

那么保存的时候是保存地址，又指向函数，而每创建一个对象，都会有一个函数，每个函数都得开辟一个内

存空间，此时浪费内存了，那么如何节省内存呢，我们需要用到原型

方法放到构造函数里面，如果多次实例化，会浪费内存

什么是原型对象：就是一个属性，是构造函数的属性，这个属性是一个对象，我们也称呼，prototype 为原型对象。

每一个构造函数都有一个属性，prototype

作用：是为了共享方法，从而达到节省内存

```
function Star (uname, age) {

​		this.uname = uname;
​		this.age = age;
​		// this.sing = function () {
​		// 	console.log(this.name + '在唱歌');
​		// }

​	}
​	Star.prototype.sing = function () {
​		console.log(this.uname + '在唱歌');
​	}

​	var zxc = new Star('周星驰', 22);
​	var ldh = new Star('刘德华', 22);
​	// console.log( Star.prototype );
​	ldh.sing();
​	zxc.sing();
```

**总结：所有的公共属性写到构造函数里面，所有的公共方法写到原型对象里面**

 疑问：为何创建一个对象，都可以自动的跑到原型对象上找方法

  因为每一个对象都有一个属性，对象原型，执行原型对象

# 对象原型：____proto____

主要作用：指向prototype

构造函数和原型对象都会有一个属性__proto__ 指向构造函数的prototype 原型对象，之所以我们对象可以使用构造函数prototype 原型对象的属性和方法，就是因为对象有__proto__ 原型的存在。

**总结：每一个对象都有一个原型，作用是指向原型对象prototype**

**统一称呼：____proto____原型，prototype成为原型对象**

# constructor  构造函数

<u>**记录是哪个构造函数创建出来的**</u>

指回构造函数本身

原型（__proto__）和构造函数（prototype）原型对象里面都有一个属性constructor属性，constructor 我们称为构造函数，因为它指回构造函数本身。constructor 主要用于记录该对象引用于哪个构造函数，它可以让原型对象重新指向原来的构造函数。一般情况下，对象的方法都在构造函数的原型对象中设置。如果有多个对象的方法，我们可以给原型对象采取对象形式赋值，但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象constructor  就不再指向当前构造函数了。此时，我们可以在修改后的原型对象中，添加一个constructor 指向原来的构造函数。

# JavaScript 的成员查找机制

```
当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。

如果没有就查找它的原型（也就是__proto__指向的prototype 原型对象）。

如果还没有就查找原型对象的原型（Object的原型对象）。

依此类推一直找到Object 为止（null）。

__proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线。

// console.log(Star.prototype.__proto__.__proto__);
// console.log(Object.prototype);
```

# 继承

ES6之前并没有给我们提供extends 继承。我们可以通过构造函数+原型对象模拟实现继承，被称为组合继承

```
call()
调用这个函数, 并且修改函数运行时的this 指向
fun.call(thisArg, arg1, arg2, ...);call把父类的this指向子类
thisArg ：当前调用函数this 的指向对象
arg1，arg2：传递的其他参数
```

## **属性的继承**

```
function Father (uname,age) {
			// this指向父类的实例对象
			this.uname = uname;
			this.age = age;
			// 只要把父类的this指向子类的this既可
		}
		function Son (uname, age,score) {
			// this指向子类构造函数
			// this.uname = uname;
			// this.age = age;
			// Father(uname,age);
			Father.call(this,uname,age);
			this.score = score;
		}
		Son.prototype.sing = function () {
			console.log(this.uname + '唱歌')
		}
		var obj = new Son('刘德华',22,99);
		console.log(obj.uname);
		console.log(obj.score);
		obj.sing();
```

## 方法的继承

**实现方法把父类的实例对象保存给子类的原型对象**

```
一般情况下，对象的方法都在构造函数的原型对象中设置，通过构造函数无法继承父类方法。核心原理：

①将子类所共享的方法提取出来，让子类的prototype 原型对象= new 父类()  

②本质：子类原型对象等于是实例化父类，因为父类实例化之后另外开辟空间，就不会影响原来父类原型对象

③将子类的constructor 
```

```

function Father () {
		}
		Father.prototype.chang = function () {
			console.log('唱歌');
		}
		function Son () 
		}
		// Son.prototype = Father.prototype;
		Son.prototype = new Father();
		var obj = new Son();
		obj.chang();
		Son.prototype.score = function () {
			console.log('考试');
		}
		// obj.score();
		// console.log(Son.prototype);
		console.log(Father.prototype);
```

**注意：一定要让Son指回构造函数**

```
实现继承后，让Son指回原构造函数

Son.prototype = new Father();

Son.prototype.constructor = Son;
```

**总结：用构造函数实线属性继承，用原型对象实线方法继承**

# ES5 中的新增方法

数组方法：

**forEach()**

```
array.forEach(function(currentValue, index, arr))

currentValue：数组当前项的值
index：数组当前项的索引
arr：数组对象本身
```

**filter()**

```
array.filter(function(currentValue, index, arr))

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素,主要用于筛选数组

注意它直接返回一个新数组

currentValue: 数组当前项的值

index：数组当前项的索引

arr：数组对象本身回调函数里面添加return添加返回条件
```

**some()**

```
array.some(function(currentValue, index, arr)) 【注意：找到或者满足条件立刻停止】

some() 方法用于检测数组中的元素是否满足指定条件. 通俗点查找数组中是否有满足条件的元素

注意它返回值是布尔值, 如果查找到这个元素, 就返回true , 如果查找不到就返回false.

如果找到第一个满足条件的元素,则终止循环. 不在继续查找.

currentValue: 数组当前项的值index：数组当前项的索引

arr：数组对象本身
```

# 改变函数内部this 指向

## call 方法

```
call() 方法调用一个对象。简单理解为调用函数的方式，但是它可以改变函数的this指向。

fun.call(thisArg, arg1, arg2, ...)
thisArg：在fun 函数运行时指定的this 值

arg1，arg2：传递的其他参数

返回值就是函数的返回值，因为它就是调用函数

function Father () {this}
function Son () { Father.call(this,1,2) }

因此当我们想改变this 指向，同时想调用这个函数的时候，可以使用call，比如继承
```

## apply 方法

```
fun.apply(thisArg, [argsArray]):调用函数

thisArg：在fun函数运行时指定的this值

argsArray：传递的值，必须包含在数组里面

返回值就是函数的返回值，因为它就是调用函数

因此apply 主要跟数组有关系，比如使用Math.max() 求数组的最大值
    var arr = [23,45,56,23,54];

	var n = Math.max.apply(null,arr);

	console.log(n);
```

## bind 方法

```
bind() 方法不会调用函数。但是能改变函数内部this 指向

fun.bind(thisArg, arg1, arg2, ...)

thisArg：在fun 函数运行时指定的this 值

arg1，arg2：传递的其他参数

返回由指定的this 值和初始化参数改造的原函数拷贝

因此当我们只是想改变this 指向，并且不想调用这个函数的时候，可以使用bind
var btn = document.querySelector('input');

		btn.onclick = function () {
			this.disabled = true;
			window.setTimeout(function () {
				this.disabled = false;
			}.bind(btn),2000);
	}
```

```
相同点:  都可以改变函数内部的this指向.

区别点:  
1.call 和apply  会调用函数, 并且改变函数内部this指向.
2.call 和apply 传递的参数不一样, call 传递参数aru1, aru2..形式apply 必须数组形式[arg]
3.bind  不会调用函数, 可以改变函数内部this指向

主要应用场景:  
1.call 经常做继承. 
2.apply 经常跟数组有关系.比如借助于数学对象实现数组最大值最小值
3.bind  不调用函数,但是还想改变this指向. 比如改变定时器内部的this指向
```

# 高阶函数

把函数作为参数，或者把函数作为返回值的的函数，称为高阶函数

# 闭包

*闭包作用：延伸变量的作用范围。*

闭包（closure）指有权访问另一个函数作用域中变量的函数。【很多种解释，都并不权威】

简单理解就是，一个作用域可以访问另外一个函数内部的局部变量。

```
var name = "The Window";
   var object = {
     name: "My Object",
     getNameFunc: function() {
     return function() {
     return this.name;
     };
   }
 };
console.log(object.getNameFunc()())    "The Window"
```

```
var name = "The Window";　　
  var object = {　　　　
    name: "My Object",
    getNameFunc: function() {
    var that = this;
    return function() {
    return that.name;
    };
  }
};
console.log(object.getNameFunc()())
```

# 递归

递归：如果一个函数在内部可以调用其本身，那么这个函数就是递归函数。简单理解:函数内部自己调用自己, 这个函数就是递归函数

由于递归很容易发生“栈溢出”错误（stack overflow），所以必须要加退出条件return。

```
利用递归求1~n的任意一个数的阶乘
//利用递归函数求1~n的阶乘 1 * 2 * 3 * 4 * ..n
 function fn(n) {
     if (n == 1) { //结束条件
       return 1;
     }
     return n * fn(n - 1);
 }
 console.log(fn(3));
```

# 深拷贝和浅拷贝

## 浅拷贝：

```
var obj = {
			name : '张三丰',
			age : 22
		};

		var newObj = {};
		for (key in obj) {
			newObj[key] = obj[key];
		}

		console.log(newObj);
		
es6：新方法

Object.assign(target, sources);

console.log(newObj);

```

## 深拷贝

```
var obj = {
			name : '1张三丰',
			age : 22,
			messige : {
				sex : '男',
				score : 16
			},
			color : ['red','purple','qing']

		}

		var newObj = {};


		function kaobei (newObj,obj) {

			for (key in obj) {

				if (obj[key] instanceof Array) {
					newObj[key] = [];
					kaobei(newObj[key],obj[key]);
				} else if (obj[key] instanceof Object) {
					newObj[key] = {};
					kaobei(newObj[key],obj[key])
				} else {
					newObj[key] = obj[key];
				}

			}

		}
		obj.messige.sex = 99;
		kaobei(newObj,obj);
		console.log(newObj);
```

# 正则表达式概述

```
正则表达式（ Regular Expression ）是用于匹配字符串中字符组合的模式。在JavaScript中，正则表达式也是对象。
作用：检索关键字，过滤敏感字符，表单验证
正则表通常被用来检索、替换那些符合某个模式（规则）的文本，例如验证表单：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文(匹配)。此外，正则表达式还常用于过滤掉页面内容中的一些敏感词(替换)，或从字符串中获取我们想要的特定部分(提取)等 。
```

## **创建正则表达式**

```
在 JavaScript 中，可以通过两种方式创建一个正则表达式
方式一：通过调用RegExp对象的构造函数创建 

    var regexp = new RegExp(/123/);
    console.log(regexp);
方式二：利用字面量创建 正则表达式

     var reg = /abc/; 含义：只要包含abc就可以
```

## 测试正则表达式

```
test() 正则对象方法，用于检测字符串是否符合该规则，该对象会返回 true 或 false，其参数是测试字符串

注意正则里面没有引号
regexObj.test(str);
regexObj：正则表达式
str：用户输入字符串

var rg = /123/;
console.log(rg.test(123));//匹配字符中是否出现123  出现结果为true
console.log(rg.test('abc'));//匹配字符中是否出现123 未出现结果为false
```

## 边界符

```
正则表达式中的边界符（位置符）用来提示字符所处的位置，主要有两个字符
^ : 表示匹配行首的文本（以谁开始）【/^abc/：以abc为开头】
$：表示匹配行尾的文本（以谁结束）【/^abc$/：只能是abc】
如果 ^和 $ 在一起，表示必须是精确匹配
```

## [] 方括号

表示有一系列字符可供选择，只要匹配其中一个就可以了【多选1】

取反 方括号内部加上 ^ 表示取反，只要包含方括号内的字符，都返回 false 。

/^[^a-z]$/：两个^，括号外面的是便边界，括号里面的是取反的含义

## 符

```
量词		说明

*		重复0次或更多次【>=0次】/^[a-z]*$/

+		重复1次或更多次【>=1次】【/^[a-z]+$/】

?		重复0次或1次

{n}		重复n次

{n,}	重复n次或更多次

{n,m}	重复n到m次
注意：{n,m}n和m之间不准有空格

边界符：^，$
中括号：[]：被中括号包含的东西只能选1个
量词符：*，+，?，{n,m}
```

## replace替换

```
stringObject.replace(regexp/substr,replacement)
```

返回值

一个新的字符串，是用 *replacement* 替换了 regexp 的第一次匹配或所有匹配之后得到的。