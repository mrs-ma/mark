# flex介绍

移动端首选flex ,PC 不考虑兼容情况 可以flex

**使用思想上和传统盒子完全不同，不要再想子元素是块级元素、行内元素等**，

加在父级  容器上面

# flex-容器属性

## flex-direction（确认主轴的方向）

flex-direction: column-reverse;（主轴：列，从下到上）

## justify-content（控制子元素在主轴上对齐方式）

 flex-start：默认值，从主轴头部开始

 flex-end: 从尾部开始对齐

center：居中对齐

space-around:剩余空间环绕在子元素周围

## flex-wrap（控制子元素是否换行）

默认不换行，如果子项目的加起来的总宽超过父亲的宽度，子项目的宽度会被合理的压缩

flex-wrap: wrap;换行

## align-items（控制子元素（项目）整体在侧轴上对齐方式）

 align-items: flex-start 侧轴的头部开始对齐

 align-items: flex-end  侧轴的尾部开始对齐

 align-items: center     侧轴上居中

 align-items: stretch    在侧轴方向上进行拉伸（规则：如果在侧轴方向上进行拉伸，CSS设置子元素不能在侧轴方                           向有大小的设置 ， 如果子元素在侧轴方向有大小的设置，拉伸不生效 ）
      

## align-content（控制子元素（多行）在侧轴上对齐方式）

# 项目属性

## flex-使用1（flex划分主轴上剩余空间给子元素）


​    圣杯布局第3种方案

     .p {
          width: 100%;
          height: 100px;
          border: 1px solid #000;
          display: flex;
          /* row */
        }
        
    .left {
      width: 100px;
      height: 100px;
      background-color: #ccc;
    }
    
    .mid {
      /* 把主轴上剩余空间 全部占有 吃掉 */
      flex: 2;
      height: 80px;
      background-color: pink;
    }
    
    .right {
      width: 100px;
      height: 100px;
      background-color: #ccc;
    }
## align-self（控制单个项目（子元素）在侧轴上自己的对齐方式；）

默认值auto，如果父级设置了align-items ，auto继承父级元素上设置侧轴的对齐方式：align-items 属性；

​                        如果父级没有设置align-items 属性，auto默认值会变为strecth；（注意侧轴方向上控制元素大小的   

​                        CSS设置要注释掉）