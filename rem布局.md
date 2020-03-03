# rem布局

## rem单位

rem：等比目的  1rem：HTML font-size设置大小??px；

只要根基1rem背后代表的具体的值会变的话，页面上所有用到rem的单位的属性都会跟着变，等比变化；

## rem布局-问题解决

如果UI给540px 设计稿？如何选择1rem 背后代表的值？

* 540px设计稿必定要在众多等比变化的效果中显示的一个；
* 必定在某个媒体查询的档位下进行显示；当前这个档位下的rem 背后代表的值就是我们需要的值；
* 1rem = 54px;
* 如果给你的540px宽度设计稿，540px = 540 / 54 = 10rem；
* 页面中其他元素：44 px  =  44 / 54  = 0.8148148148148148 ‬rem;

## rem布局-问题解决  计算引出的LESS

less:CSS预处理语言，不能直接用，转后的CSS文件

1.正常写

```
body {
  width: 100%;
  min-width: 320px;
}

div {
  background-color: #ccc;
}
```

2.变量

```
@bg:#ccc;
header {
  background-color: @bg;
}

.banner {
  color: @bg;
}

span {
  border:10px solid @bg;
}
```

3.嵌套 HTML结构

```
header {
  height: 44px;
  border-bottom: 1px solid #ccc;
  display: flex;
  .left {
    width: 40px;
    background-color: pink;
  }
  .mid {
    flex:1
  }
  .right {
    width: 40px;
    background-color: #222;
  }
  div {
    background-color: #ccc;
    // &：代表当前这个CSS的自己 div
    &:hover {
      background-color: #333;
    }
    &::before {
      content:"";
    }
  }
  // div:hover {
  //   background-color: #222;
  // }
}
```

4.计算

```
div {
  width: 60px+20px;
  height: 60px/20px;
  height: 60px*20px;
  height: (60-38)/2*20px;
  // 单位如何使？单位不参与运算，选择一个单位；
  // 两个不同的单位，选前面那个单位
  height: 44px/54rem;
  height: 44/54rem;
}
```

# rem布局-方案

## 构建文件目录及初始化

<!-- 初始化base -->
  <link rel="stylesheet" href="./css/normalize.css">

  <!-- commom.css 公共的啥？各个档位下rem  -->
  <link rel="stylesheet" href="./css/commom.css">

  <!-- 生成的CSS文件，看less文件 -->
  <link rel="stylesheet" href="./css/index.css">

# rem&flexible.js

帮助我们实现，连续变化，帮我们实现了430个档位；

0-正无穷大 每个档位都给我了；（需要的是：320-750）

flexible.js去实现连续变化，也是上面的430个档位；引入页面内；不需要common.css

```
@media screen and (max-width:319px) {
  html {
    font-size: 32px!important;
  }
}

@media screen and (min-width:750px) {
  html {
    font-size: 75px!important;
  }
}
```

