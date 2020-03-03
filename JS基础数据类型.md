# JS基础

## js-数据-5种简单值类型

 1.number 类型

```
 var a = 10.1;
 var b = NaN;
 NaN：不是某个数，泛指，不确定；
```

2.String 类型：字符串（规则：只要两边有单双引号的一种，这个就是String 类型，就是个字符串）

```
var info = '我说：\"xxxxxxx\" ;  他说:\'xxxxxxxxx1\';     她说：\\  ';转义字符
```

 3.boolean 类型：描述一件事 对或者错？存在？确定？

4.Null值;

5.Undefined类型

## js-数据-检查类型

var aType = typeof(a)

 var aType = typeof a

# js-转化-转数字

其他 变 数字

String  var jx = "1500.1"    jx = Number(jx);

​             var a = "abc"             a = Number(a)     =>NaN

Boolean      var a = true        a = Number(a)

parseInt()方法 :返回：整数部分；
传入：参数，转成功的话，只能传入数字部分在前的字符串；
           传入是其他（和上面不一样）,返回NaN；

parseFloat()方法:返回值：整数加小数部分；
 传入：转成功的话，只能传入数字部分在前的字符串；

## js-转化-转字符串

Number ----->String

var a = NaN   a = String(a)

.toString()方法 

var a = 10   a = a.toString()  null，undefined不能用.tostring()方法

## js-转化-转Boolean

转化为false的几种情况:

```
var res1 = Boolean(0);
var res3 = Boolean(NaN);
var res2 = Boolean('');  // 空字符，里面啥没有，空格也没有；
var res6 = Boolean(false);
var res5 = Boolean(null);  
console.log(res5); //输出false
var res4 = Boolean(undefined); 
console.log(res4); //输出false
```

# js-操作符

## 算术操作符

字符串 遇见 +，使临近字符串的其他数据类型，转化为字符串，形成字符串拼接

字符串 遇见` - * / %` ,字符串会隐式转化Number类型；

`++  --`：作用：在自己的基础上进行自增1，或自减1；

如果遇见++写在a的后面，先把自己的数推到位置上，在进行a++运算（运算后结果不推到位置上）

如果遇见++写在a前面，++a先算，计算后的结果，再往位置上提供数据

## 比较运算符

常规操作：左右需要Number类型；

非常规操作 规则：非Number类型要和Number类型比较的话，非Number类型就要隐式转换为Number类型；

== 规则：
  1.如果两边的数据类型不同，非Number类型转Number类型，看值是否相同；
  2.如果两边的数据类型相同，看值是否相等；

=== 规则：(严格，没有隐式转化)
  1.直接先看数据类型，如果数据类型不同，直接返回false;
  2.如果两边的数据类型相同，看值是否相等；

## 逻辑运算符

&& 
   且：全部满足，如果有一个条件不满足，直接返回不满足的结果;
   执行过程：&& 前后 每个位置上需要一个数据 （Boolean类型）只进行比较，不返回；
   返回： 最后成立的结果 或 不成立的结果；

 || 或：只要满足一个条件就可以；
      返回：满足条件的结果；

## 操作符-优先级



  1.第一优先级：()

  2.第二优先级：++ -- !

  3.第三优先级： * /  %

  4.第四优先级： + -

  5.第五优先级： > >= < <=

  6.第六优先级： == != === !==

  7.第七优先级： &&

  8.第八优先级： ||

  9.第九优先级： = += -= *= /= %=  

