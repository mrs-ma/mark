# WebApi

## js组成：

ES

DOM：文档当做成为**对象模型**，树状结构当做对象模型

* DOM节点（JS的叫法）：HTML里面标签（标签属性、标签内的文本）；

 BOM：浏览器当做一个**对象**；

## DOM-获取（Id)

作用: 获取页面中  已经存在  的HTML标签,DOM节点,元素对象;
参数:字符串 id 值；
返回:DOM节点（元素对象）,如果页面中没有这个DOM节点，返回null(复杂数据类型，代表空);  

元素对象---->属性和方法的集合；

var btn = document.getElementById("btn");

 var body = document.body;

###  DOM事件

onclick   onfocus  onblur

例：search.onfocus = function() {
    list.style.display = "block";
  };

### DOM-属性-类名-className

className：属性，获取和设置DOM节点上的class

例：  

```
var btn = document.getElementById("btn");
  btn.onclick = function() {
    div.className += " bg-red";
  };
```

### DOM-属性-类对象-classList

.add()   .remove()   .toggle()

例：

```
 var btn = document.getElementById("btn");
  btn.onclick = function() {
    box.classList.add("bg-red");
  };
```

## DOM-获取ByTagName和ByClassName

参数：TagName 标签名 字符串；
返回：拥有标签名的伪数组，成员是DOM节点；  for循环；

 var ipts = document.getElementsByTagName("input");
  console.log(ipts);

 getElementsByClassName
 参数：ClassName 类名 字符串；
 返回：拥有类名的伪数组，成员是DOM节点；  for循环；
  var btns = document.getElementsByClassName("btn");
  console.log(btns);

## 自定义属性

自定义属性名字： data-自己命名 = 值;

获取：DOM节点.dataset属性名，背后值是一个对象，对象上有刚才自定义的 属性abc 和 值"1"；

意义：一般要标签 btn和 某个数据(图片地址) 形参一一对应关系，放在自定义属性里；

## DOM-属性checked

属性：开关属性： checked/selected/disabled ，这种只有两种状态的属性；`<input type="checkbox" name="check" id="ck"  />`

获取：DOM.checked

设置：`ck.checked = true;` 两个状态的值，布尔类型；

## DOM-案例-全选与取消

```
 var all = document.getElementById("checkAll");
  var cks = document.getElementsByClassName("ck"); // 伪数组 
  all.onclick = function() {
    var flag = all.checked;  
    // 把all 状态给每一个子ck上；
    for (var i = 0; i < cks.length; i++) {
      cks[i].checked = flag;
    }
  }
```

需求2：子选项 的变化 会使大选择框的状态的改变

```
 for (var i = 0; i < cks.length; i++) {
    cks[i].onclick = function() {
      // 三兄弟状态的判断：每一个兄弟状态看一次；
      for (var j = 0; j < cks.length; j++) {
        // 如果有一个兄弟，没有选中。没有必要继续循环 
        if (cks[j].checked == false) {
          break;
        }
      }

      // 如果j==cks.length ,上面的循环全部完成，没有一个进入终止，没有一个执行  cks[j].checked == false
      if (j == cks.length) {
        all.checked = true;
      }
      // j!=cks.length 上面的循环没有完成，意味循环被终止，有一个子ck 执行 cks[j].checked == false
      else {
        all.checked = false;
      }
    }
  }
```

# DOM-获取-CSS选择器

 var box = document.querySelector("#box");

var fs = document.querySelectorAll(".father");

## DOM-属性-操作属性的方法

参数：第一个自定义属性名，第二个自定义属性值；

 var c = box.setAttribute("abc", "----------------------");

获取

 var a = box.getAttribute("abc");

删除

 box.removeAttribute("abc");

## 事件-注册addEventListener

**可以多次注册事件，不会前后覆盖；**

```
 btn.addEventListener("click", function() {
    alert(1);
  });
```

# DOM-事件-三个阶段-冒泡与捕获

  事件执行3个阶段：捕获、到达目标、冒泡
  捕获：从根部节点一层一层往上找，直到找到我们刚才触发的那个节点，这个过程叫捕获；
  到达目标：找到我们刚才触发的那个节点
  冒泡：从找的目标节点，一层一层往往根节点找，这个过程叫冒泡

  事件默认是在冒泡阶段执行；在冒泡的阶段，发现父级节点们也注册和用户触发的行为一样的事件，这些事件函            数被执行，同样， 如果孙子没有点击事件， 但是用户对孙子有  点击行为  ，但是爷爷注册有点击事件， 爷爷同样       也会触发点击事件。

 e.stopPropagation(); 阻止冒泡行为；

# DOM-事件对象

e.clientX, e.clientY  参照当前可视窗口左上角为基准点

e.pageX, e.pageY    参照与body为左上角为基准点

e.target                     点击是谁就是谁

e.currentTarget        当前，事件注册给谁就是谁；

 e.preventDefault();  阻止默认行为

# DOM-事件-委托

新属性：innerHTML    ul.innerHTML += '<li class="son">-------------------</li>';

什么是事件委托？

把事件注册在父级的元素身上，

利用事件冒泡执行，当事件传播到已经注册了事件的父级元素身上，

判断  触发事件的DOM  （e.target）节点是否是指定的元素，e.target---->DOM节点

e.target.nodeName=="LI"      nodeName：节点的大写名称；

# DOM-事件-鼠标

  

```
// 鼠标在某个元素上 落下的时候，触发
  box.addEventListener("mousedown", function() {
    console.log(1);
  });

  // 鼠标在某个元素上 移动，触发
  box.addEventListener("mousemove", function() {
    console.log(2);
  });

  // 鼠标在某个元素上 弹起 触发
  box.addEventListener("mouseup", function() {
    console.log(3);
  });
```

DOM.offsetTop;  与有定位的父级的  水平和垂直距离

## 案例-鼠标拖盒子动



    // 需求：拖动
      // 分析：拖动到任何地方，鼠标在盒子内的位置一直没有变；
    
      // 声明一个变量，通过代码控制变量不同的情况，不同的值，开关思想；
      var kaiguan;
      // 步骤：
      // 1.谁？获取DOM节点？
      var box = document.querySelector(".box");
    
      var x_start, y_start;
      // 2.鼠标落下：把鼠标在盒子内的位置，记住（找个变量接受）；
      box.onmousedown = function(e) {
        // 鼠标的位置-盒子的位置；
        // 鼠标的位置：事件对象e  e.pageX
        // 盒子的位置:box.offsetLeft
    kaiguan = "按下";
    // 鼠标在盒子内水平距离；
    x_start = e.pageX - box.offsetLeft;
    y_start = e.pageY - box.offsetTop;
      };
    
      // 3.mousemove :document
      document.onmousemove = function(e) {
        // 盒子的新位置 = 鼠标的新位置-鼠标在盒子内的位置；
        // 鼠标的新位置：e事件对象  e.pageX
        // 鼠标在盒子内的位置  x_start  y_start;
        // console.log(kaiguan);
        if (kaiguan == "弹起") {
          // 下面的代码不再执行，不再移动；
          return;
        }
    // 设置：
    box.style.left = e.pageX - x_start + "px";
    box.style.top = e.pageY - y_start + "px";
     }
    
      // 问题：鼠标弹起后，mousemove这个事件不能再执行了
      // 思想：开关思想
      box.onmouseup = function() {
        kaiguan = "弹起";
      };
    
      // 问题2：再次按下的鼠标的时候。kaiguan： "弹起"，移动不再执行；



# 事件解绑

 btn.removeEventListener('click',fn);

btn.onclick=null

 

# DOM-节点-修改、创建、添加

创建：

* innerHTML属性：可以识别HTML结构；
* document.write();  可以识别HTML结构；
* document.createElement('li') ：在JS里面创建出DOM节点，只是创建，不显示在页面；

添加：

* 父节节点.appendChild(新DOM节点)：从后添加新的DOM节点；
* 父节节点.insertBefore(新DOM节点，插入谁之前的DOM节点)：在某个元素之前，添加新的DOM节点

修改DOM内部结构或者文本：

* innerHTML：结构；
* innerText：文本内容；

# DOM-节点-通过节点获取节点

```
// 
  var ul = document.querySelector("ul");

  // 属性：children 伪数组；
  // console.log(ul.children[0]);


  // 属性：获取父级DOM节点 找上级父级
  var li3 = document.querySelector("#li3");
  // console.log(li3.parentNode);
  // // 找定位父亲，没有--->body
  // console.log(li3.offsetParent);


  // 属性：获取兄弟元素,下一个兄弟
  console.log(li3.nextElementSibling);
  console.log(li3.previousElementSibling);
```

# DOM-节点-删除

```
// 谁调用：指定父级，删除某个子元素；
    // 参数：被指定的子元素；
    ul.removeChild(ul.children[0]); 
```

# BOM-window及onload

BOM 把浏览器看成对象

onload:注册，事件，什么时候执行？页面静态资源加载完毕时才会执行；
 静态资源：css img 文件；页面中有图片，使用 window.onload 把所有的代码包起来；

```
 window.onload = function() {
    // 加载之后，JS代码了’
  }
```

# BOM-定时器

一次性定时器  

setTimeout  是window上的方法。
参数：倒计时执行函数；
第一个：执行函数；
第二个：倒计时 默认单位是ms  1s = 1000ms；

  // 返回值：返回一个number值，用于清除定时器；

永久性定时器

   Interval：间隔,等待间隔后的时间才执行；
 参数：
 第一个：执行函数；
 第二个：事件间隔 默认单位是ms  1s = 1000ms；

# location

语法：负责管理浏览器地址栏相关的行为和信息的对象；

 对象（属性和方法） 属性href：获取和设置地址；

```
 setTimeout(function() {
    // JS通过属性控制页面转跳
    location.href = "http://www.baidu.com";
  }, 2000);
```

# localStorage

作用：小U盘，浏览器自带的；20M

方法：存入
参数1：存入本地哪个字段内。什么名字；键；位置；
参数2：存入的数据
真实存入（本地浏览器、小U盘）数据：

 localStorage.setItem("a", "---------------------");

方法：拿出真实存的数据；
参数：键，位置；

返回：读取的数据；

如果读取一个不存在的数据，返回null;
var info = localStorage.getItem("c");

 方法：真实清除某条数据
参数：键，位置；
localStorage.removeItem("b");

 方法：全部清除；
 localStorage.clear();

**记住：localStorage 存入复杂数据类型，要先转换为 JSON格式的字符串；**

var str = JSON.stringify(obj_1);    作用:把对象类型转换为字符串； 字符串化

 var obj_2 = JSON.parse(str_1);    作用：把JSON格式字符串转为对象

# DOM-节点-实际显示的宽高

特点：返回都是数字

offsetWidth=width+padding+border

offsetHeight

offsetLeft  距离offsetParent offsetParent(定位父亲，没有往上找，直到body) 水平距离

offsetTop

clientWidth的实际宽度   clientWidth = width+左右padding

# 无缝轮播图

**无缝原理：**

- 当我们划到6.jpg时（实际上在HTML顺序上是倒数第二张），让用户觉得已经到最后一张了。
- 再往左划时，会划出来1.jpg（实际上在HTML顺序上是最后一张），让用户觉得到无缝到了第一张了。
- 这个瞬间，最后一张图片会有个过渡；

**这个时候，我们通过一个事件（当过渡结束时），我们一瞬间把整个管理图片的父亲的位置归到1.jpg（实际上在HTML顺序上是第二张）的位置；这样就无缝完成！**

```
// 1.当过渡结束时执行函数
  var box = document.querySelector(".box");

  // box.addEventListener("transitionend", function() {
  //   console.log(1);
  // });

  
  // 2.动画结束时执行；
  box.addEventListener("animationend", function() {
    console.log("------------------");
  });
```



swiper轮播图