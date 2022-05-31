---
title: flex
date: 2022-05-18 16:30:34
tags: CSS
---

#### flex弹性盒、伸缩盒

是CSS中又一种布局手段，它主要用来代替浮动完成页面的布局；flex可以使元素具有弹性，让元素跟随页面的大小的改变而改变

要使用弹性盒，必须先将一个元素设置为弹性容器

```css
display:flex  设置块级弹性容器
display:inline-flex  设置行内的弹性容器
```

弹性元素

​	弹性容器的直接子元素使弹性元素（弹性项）

​	一个元素可以同时是弹性容器和弹性元素

`flex-direction `指定容器中弹性元素的排列方式

可选值：row 默认值，弹性元素自左向右水平排列；主轴 自左向右

​				row-reverse  反向水平排列自右向左

​				column   纵向排列，自上向下

​				column-reverse  反向纵向排列，自下向上

主轴：弹性元素的排列方向称为主轴

侧轴：与主轴垂直的方向称为侧轴



弹性元素的属性：

​	flex-grow  指定弹性元素的伸展系数

​		当父元素有多余的空间时，子元素如何伸展，父元素的剩余空间会按照设置的比例进行分配

​	flex-shrink 指定弹性元素的收缩系数

​		当父元素中的空间不足以容纳所有子元素时，如何对子元素进行收缩

```css
	*{
            margin: 0;
            padding: 0;
            list-style: none;
        }
        ul{
            width: 800px;
            border: 10px solid red;
            /* 将ul变成弹性容器 */
            display: flex;
            flex-direction: row;
        }
        li{
            width: 200px;
            height: 100px;
            background-color: #bfa;
            text-align: center;
            line-height: 100px;
            font-size: 50px;
        }
        li:nth-child(2){
            background-color: pink;
            flex-grow: 0;
        }
        li:nth-child(3){
            background-color: orange;
            flex-grow: 0;
        }
```

##### 设置弹性元素是否在弹性容器中自动换行

```css
flex-wrap: nowrap;  默认值，元素不换行
flex-wrap: wrap;    元素沿着侧轴方向换行
flex-wrap: wrap-reverse;   元素沿着侧轴反方向换行
```

###### flex-flow: wrap和direction 的简写属性

```css
flex-flow: row wrap;
```

### 弹性容器的样式

##### 如何分配主轴上的空白空间（主轴上元素如何排列）

```css
justify-content: flex-start;   元素沿着主轴起边排列
justify-content: flex-end;		元素沿着主轴终边排列
justify-content: center;		元素居中排列
justify-content: space-around;	空白分布到元素两侧
justify-content: space-evenly;	空白分布到元素的单侧
justify-content: space-between;	空白均匀分布到元素间
```

##### 如何分配侧轴上的元素和空白空间

```css
align-items: stretch;    默认值，将元素长度设置为相同的值
align-items: flex-start;	元素不会拉伸，沿着侧轴起边排列
align-items: flex-end;		沿着侧轴的终边排列
align-items: center;        居中排列
align-items: baseline;		基线对齐排列
```

```css
align-content: space-between;  空白均匀分布到元素间
其他规则和主轴相同
```

### 弹性元素的样式

```css
/* 元素的基础长度
                指定的是元素在主轴上的基础长度
                主轴是横向，则是宽度
                主轴纵向，则是高度
                默认值是auto  表示参考元素自身的高度或宽度
                如果传递了具体的数值，则以该值为准
            */
            flex-basis: 100px;

```

```css
			/* 
                flex 可以设置弹性元素所有的三个样式
                flex: 增长 缩减 基础;

                initial  "flex: 0 1 auto;"
                auto     "flex: 1 1 auto;"
                none     "flex: 0 0 auto;"
            
            */
            flex: 0 1 auto;
```

order 可以决定弹性元素的排列方式

```css
	li:nth-child(1){
            background-color: pink;
            order: 3;
        }
        li:nth-child(2){
            background-color: pink;
            order: 2;
        }
        li:nth-child(3){
            background-color: orange;
            order: 1;
        }
```

#### 像素

像素：

​	屏幕是由一个一个发光的小点构成，这一个个小点就是像素

​	分辨率：1920 x 1080 说的就是屏幕中小点的数量

在前端开发中像素要分成两种情况讨论：CSS像素和 物理像素

物理像素，上述所说的小点就属于物理像素

CSS像素：编写网页时，我们所用像素都是CSS像素

​	浏览器显示网页时需要将CSS像素转换为物理像素然后再呈现

​	一个CSS像素最终由几个物理像素显示，由浏览器决定：

​			默认情况下在pc端，一个CSS像素=一个物理像素



视口（viewport）

​	视口就是屏幕中用来显示网页的区域

可以通过查看视口的大小，来观察CSS像素和物理像素的比例

默认情况下

​	视口宽度 1920px(CSS像素)

​					1920px（物理像素）

​			CSS像素和物理像素比值是1：1



放大两倍的情况：

​	视口宽度 960px(CSS像素)

​					1920px（物理像素）

​			CSS像素和物理像素比值是1：2

#### 手机像素

在不同的屏幕，单位像素的大小是不同的，像素越小屏幕会越清晰

24寸   1920 X 1080

iPhone6  4.7寸    750 X 1334

智能手机的像素点远远小于计算机的像素点

问题：一个宽度为900px的网页在iPhone6中如何显示呢？

默认情况下，移动端的网页都会将视口设置为980px（CSS像素）

以确保pc端网页可以在移动端正常访问，但是如果网页的宽度超过980，移动端的浏览器会自动对网页进行缩放以完整显示网页



#### 完美视口

`<meta name="viewport" content="width=device-width">  ` 设置视口大小，device-width表示设备的宽度（完美视口）



#### vw单位

vw表示的是视口的宽度

100vw=一个视口的宽度

1vw=1%视口的宽度

vw这个单位永远相对于视口宽度进行计算

```css
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        html{
            /* 网页中字体大小最小是12px,不能设置一个比12px还小的字体 */
            /* 0.1333333333333333vw=1px */
            /* font-size: 0.1333333333333333vw; */

            /* 5.33333vw=40px */
            font-size: 5.33333vw;
        }
        .box1{
            /* 1 rem=1 html的字体大小 */
            width: 18.75rem;   /*750px*/
            height: 0.875rem;
            background-color: #bfa;
        }
    </style>
</head>
<body>
    <div class="box1"></div>
</body>
</html>
```



#### 媒体查询

响应式布局

​	网页可以根据不同的设备或窗口大小呈现出不同的效果；使用响应式布局，可以使一个网页适用于所有设备



媒体查询：

语法： @media 查询规则{}

​		媒体类型：

​			all 所有设备

​			print 打印设备

​			screen 带屏幕的设备

​			speech 屏幕阅读器

可以使用逗号连接多个媒体类型，这样它们之间就是一个或的关系

可以在媒体类型前面加个only  兼容一些老的浏览器

```css
@media only screen{
    body{
        background-color: #bfa;
    }
}
```

