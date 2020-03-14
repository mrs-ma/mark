# 		JQuery

jQuery 是一个快速、简洁的 JavaScript 库

​	JavaScript库：即 library，是一个封装好的特定的集合（方法和函数）。

​	学习jQuery本质： 就是学习调用这些函数（方法）。【方法()】

链式编程、隐式迭代

# jQuery入门

## **jQuery** **的入口函数**

第一种：

```
$(function () {   
    ...  // 此处是页面 DOM 加载完成的入口
 }) ;
```

第二种：

```
$(document).ready(function(){
   ...  //  此处是页面DOM加载完成的入口
});       

```

等着 DOM 结构渲染完毕即可执行内部代码，不必等到所有外部资源加载完成，jQuery 帮我们完成了封装。

不同于原生 js 中的 load 事件是等页面文档、外部的js 文件、css文件、图片加载完毕才执行内部代码。

更推荐使用第一种方式。

## **jQuery** **对象和** **DOM** **对象**

用原生 JS 获取来的对象就是 DOM 对象【document.getElement等方法】

jQuery 方法获取的元素就是 jQuery 对象【$('div')等】

jQuery 对象本质是： 利用$对DOM 对象包装后产生的对象（伪数组形式存储）

特别注意:只有 jQuery 对象才能使用 jQuery 方法，DOM 对象则使用原生的 JavaScirpt 方法。

## 相互转换

DOM 对象转换为 jQuery 对象： $(DOM对象)

jQuery 对象转换为 DOM 对象（两种方式）

​	$('div') [index]       index 是索引号 

​	$('div') .get(index)    index 是索引号

# **jQuery** 常用API

## *jQuery选择器*

**$(“选择器”)   // 里面选择器直接写 CSS 选择器即可，但是要加引号**     

```
$('#id')==》指定id元素

$('*')==》所有元素

$('.class')==》指定class元素

$('div')==》根据标签获取元素

$('div,p,li')==》获取多个

$('li.class')==>交集获取

$('ul>li')==>子代

$('ul li')==>后代
```

**隐式迭代**:遍历内部 DOM 元素（伪数组形式存储）的过程就叫做**隐式迭代**

## **jQuery** **筛选选择器**

$('li:first')：第一个元素

$('li:last')：最后一个元素

$('li:eq(2)')==》索引为2【查找指定索引的元素】

$('li:odd')==》索引为奇数

$('li:even')==》索引为偶数

注意：索引是从0开始的

## **jQuery** **筛选方法（重点）**

$('选择器').方法()

$('li').parent()父级

$('ul').children('li');子集【如果不加参数，获取所有的，如果添加指定的元素，按照指定的找】

$('ul').find('li')后代

$('li').siblings('li')兄弟

$('li'),nextAll();后面的

$('li').prevAll();前面的

判断是否具有某个类名：$('div').hasClass('aaa')

$('div').eq(index);指定索引方法【eq推荐用方法】

## **jQuery** **样式操作**

### **操作** **css** **方法**

```
参数只写属性名，则是返回属性值【$(this).css(''color'');】

参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号【$(this).css(''color'', ''red'');】

参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开， 属性可以不用加引号，
【$(this).css({ "color":"white","font-size":"20px"});】

```

### 设置类样式方法

作用等同于以前的 classList，可以操作类样式，注意操作类里面的参数不要加点

```
添加类【$(“div”).addClass(''current'');】

移除类【$(“div”).removeClass(''current'');】

切换类【$(“div”).toggleClass(''current'');】


原生 JS 中 className 会覆盖元素原先里面的类名。
jQuery 里面类操作只是对指定类进行操作，不影响原先的类名
```

## **jQuery** **效果**

**显示隐藏效果**

```
show([speed,[easing],[fn]])
hide([speed,[easing],[fn]])
toggle([speed,[easing],[fn]])


（1）参数都可以省略， 无动画直接显示。
（2）speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
（3）easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
（4）fn:  回调函数，在动画完成时执行的函数，每个元素执行一次。

```

**滑动效果**

```
slideDown([speed,[easing],[fn]])【显示】
slideUp([speed,[easing],[fn]])【隐藏】
slideToggle([speed,[easing],[fn]])


（1）参数都可以省略。
（2）speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
（3）easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
（4）fn:  回调函数，在动画完成时执行的函数，每个元素执行一次
```

**事件切换**

**hover([over,]out)**

```
（1）over:鼠标移到元素上要触发的函数（相当于mouseenter）

（2）out:鼠标移出元素要触发的函数（相当于mouseleave）

（3）如果只写一个函数，则鼠标经过和离开都会触发它
```

**动画队列及其停止排队方法**

```
动W或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。

停止排队:stop()

(1）stop() 方法用于停止动画或效果。

(2)  注意： stop() 写到动画或者效果的前面， 相当于停止结束上一次的动画
```

**淡入淡出效果**

```
fadeIn([speed,[easing],[fn]])
fadeOut([speed,[easing],[fn]])
fadeToggle([speed,[easing],[fn]])
fadeTo([[speed],opacity,[easing],[fn]])


（1）参数都可以省略。
（2）speed：三种预定速度之一的字符串(“slow”,“normal”, or “fast”)或表示动画时长的毫秒数值(如：1000)。
（3）easing：(Optional) 用来指定切换效果，默认是“swing”，可用参数“linear”。
（4）fn:  回调函数，在动画完成时执行的函数，每个元素执行一次。
注意：fadeTo([[speed],opacity,[easing],[fn]])
```

## **jQuery** **属性操作**

**设置或获取元素固有属性值** **prop()**

**获取语法：**

> prop(''属性'')

**设置属性语法**

> prop(''属性'', ''属性值'')

**设置或获取元素自定义属性值** **attr()**

**获取属性语法**

attr(''属性'')      // 类似原生 getAttribute()

**设置属性语法**

attr(''属性'', ''属性值'')   //类似原生 setAttribute()

**数据缓存** **data()**

当做变量存储

```
data() 方法可以在指定的元素上存取数据，并不会修改 DOM 元素结构，所以元素上无法查看。一旦页面刷新，之前存放的数据都将被移除。
```

 **附加数据语法**

data(''name'',''value'')   // 向被选元素附加数据   

**获取数据语法**

date(''name'')             //   向被选元素获取数据   

## **jQuery** **内容文本值**

**普通元素内容** **html()****（相当于原生inner HTML)

​	获取：html()   // 获取元素的内容

​	设置：html(''内容'')   // 设置元素的内容

**普通元素文本内容** **text()   (****相当与原生** **innerText****)**

​	获取：text()   // 获取元素的文本内容

​	设置：text(''文本内容'')   // 设置元素的文本内容

**表单的值** **val()****（ 相当于原生****value)**

​	获取：val()   // 获取表单的值

​	设置：val(''内容'')  // 设置表单的值

## **jQuery** **元素操作**

**遍历元素**

jQuery 隐式迭代是对同一类元素做了同样的操作。如果想要给同一类元素做不同操作，就需要用到遍历。

> 语法1：$("div").each(function(index, domEle) { xxx; }）

```
\1. each() 方法遍历匹配的每一个元素。主要用DOM处理。 each 每一个

\2. 里面的回调函数有2个参数：  index 是每个元素的索引号;  demEle 是每个DOM元素对象，不是jquery对象

\3. 所以要想使用jquery方法，需要给这个dom元素转换为jquery对象  $(domEle)
```

语法2：$.each(object，function(index, element){ xxx;}）

```
\1. $.each()方法可用于遍历任何对象。主要用于数据处理，比如数组，对象

\2. 里面的函数有2个参数：  index 是每个元素的索引号;  element  遍历内容
```

**创建元素**

> 语法：$(''<li></li>'');    

**添加元素**(内部添加元素，生成之后，它们是父子关系。)

> element.append(''内容'') [把内容放入匹配元素内部最后面，类似原生 appendChild。]
>
> element.prepend(''内容'') 把内容放入匹配元素内部最前面。

**外部添加**(外部添加元素，生成之后，他们是兄弟关系)

element.after(''内容'') // 把内容放入目标元素后面

element.before(''内容'')    //  把内容放入目标元素前面

**删除元素**

element.remove()   //  删除匹配的元素（本身）

element.empty()    //  删除匹配的元素集合中所有的子节点

element.html('''')   //  清空匹配的元素内容

## **jQuery** **尺寸、位置操作**

width()、height()【只算width和height】

innerWidth()、innerHeight()【包含padding+width】

outerWidth()、outerHeight()【包含padding、border、width】

outerWidth(true)、outerHeight(true)【包含padding、border、margin、width】

**offset()设置或获取元素偏移**

```
①offset() 方法设置或返回被选元素相对于**文档**的偏移坐标，跟父级没有关系。

②该方法有2个属性 left、top 。offset().top  用于获取距离文档顶部的距离，offset().left 用于获取距离文档左侧的距离。

③可以设置元素的偏移：offset({ top: 10, left: 30 });
```

**position()** 获取元素偏移

①position() 方法用于返回被选元素相对于**带有定位的父级**偏移坐标，如果父级都没有定位，则以文档为准。

②该方法有2个属性 left、top。position().top 用于获取距离定位父级顶部的距离，position().left 用于获取距离定位父级左侧的距离。

注意：该方法只能获取。

**scrollTop()、scrollLeft()设置**或获取元素被卷去的头部和**左侧**

①scrollTop() 方法设置或返回被选元素被卷去的头部。

②不跟参数是获取，参数为不带单位的数字则是设置被卷去的头部。

scroll事件：滚动事件，（谁有滚动条加给谁）

## **jQuery** **事件**

语法：element.事件(function(){})   $(“div”).click(function(){  事件处理程序 })

**事件处理** **on()** **绑定事件**:

on() 方法优势1:可以绑定多个事件，多个处理事件处理程序。

```
 $(“div”).on({

  mouseover: function(){}, 
  mouseout: function(){},

  click: function(){}  

});
```

on() 方法优势2:可以事件委派操作。

```
$('ul').on('click', 'li', function() {

​    alert('hello world!');

});    
```

on() 方法优势3：动态创建的元素，click()没有办法绑定事件，on() 可以给动态生成的元素绑定事件

```
 $(“div").on("click",”p”, function(){

​     alert("俺可以给动态生成的元素绑定事件")

 });       
```

**事件处理** **off()** **解绑事件**

```
$("p").off() // 解绑p元素所有事件处理程序

$("p").off( "click")  // 解绑p元素上面的点击事件 后面的 foo 是侦听函数名

$("ul").off("click", "li");   // 解绑事件委托
```

**自动触发事件trigger()**

有些事件希望自动触发, 比如轮播图自动播放功能跟点击右侧按钮一致。可以利用定时器自动触发右侧按钮点击事件，不必鼠标点击触发

```
element.click()
element.trigger("type")
$("p").trigger("click"); // 此时自动触发点击事件，不需要鼠标点击
element.triggerHandler(type)  
triggerHandler模式不会触发元素的默认行为，这是和前面两种的区别。
```

## **jQuery**事件对象

```
阻止默认行为：event.preventDefault()   或者 return  false 

阻止冒泡： event.stopPropagation() 
```

