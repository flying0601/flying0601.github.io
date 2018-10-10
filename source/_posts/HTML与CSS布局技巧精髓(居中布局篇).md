---
title: HTML与CSS布局技巧精髓（居中布局篇）
date: 2017-12-20 20:27:00
categories: "HTML/CSS"
tags:
     - HTML/CSS
     - 布局技巧
description: HTML与CSS布局技巧精髓的居中布局
---

前端布局非常重要的一环就是页面框架的搭建，也是最基础的一环。在页面框架的搭建之中，又有居中布局、多列布局以及全局布局，今天我们就来总结总结前端干货中的CSS布局。<!--more-->


## 居中布局

### 水平居中
#### 1）使用inline-block+text-align
（1）原理、用法
> * 原理：先将子框由块级元素改变为行内块元素，再通过设置行内块元素居中以达到水平居中。
> * 用法：对子框设置display:inline-block，对父框设置text-align:center。

（2）代码实例
```css
.child{
    display:inline-block;
}
.parent{
    text-align:center
}
   <div class="parent">
        <div class="child">DEMO</div>
    </div>
```
（3）优缺点
>* 优点：兼容性好，甚至可以兼容ie6、ie7
>* 缺点：child里的文字也会水平居中，可以在.child添加text-align:left;还原水平居中的布局方式是最常见的一种，常常用于头部、内容区、页脚，它主要的作用是控制盒子在整个页面以水平居中的方式呈现。
#### 2）使用table+margin
（1）原理、用法
>* 原理：先将子框设置为块级表格来显示（类似 ），再设置子框居中以达到水平居中。
>* 用法：对子框设置display:table，再设置margin:0 auto。

（2）代码实例
```css
.child {
    display:table;
    margin:0 auto;
}
<div class="parent">
    <div class="child">DEMO</div>
</div>
```
（3）优缺点：
>* 优点：只设置了child，ie8以上都支持
>* 缺点：不支持ie6、ie7,将div换成table

#### 3）使用absolute+transform

（1）原理、用法
>* 原理：将子框设置为绝对定位，移动子框，使子框左侧距离相对框左侧边框的距离为相对框宽度的一半，再通过向左移动子框的一半宽度以达到水平居中。当然，在此之前，我们需要设置父框为相对定位，使父框成为子框的相对框。
>* 用法：对父框设置position:relative，对子框设置position:absolute，left:50%，transform:translateX(-50%)。

（2）代码实例
```css
.parent {
    position:relative;
}
.child {
    position:absolute;
    left:50%;
 transform:translateX(-50%);
}
   <div class="parent">
        <div class="child">DEMO</div>
    </div>
```
（3）优缺点
>* 优点：居中元素不会对其他的产生影响
>* 缺点：transform属于css3内容，兼容性存在一定问题，高版本浏览器需要添加一些前缀
#### 4）使用flex+margin

（1）原理、用法
>* 原理：通过CSS3中的布局利器flex将子框转换为flex item，再设置子框居中以达到居中。
>* 用法：先将父框设置为display:flex，再设置子框margin:0 auto。

（2）代码实例
```css
.parent {
  display:flex;
  margin：0 auto;
}

<div class="parent">
    <div class="child">DEMO</div>
</div>

```
（3）优缺点
>* 缺点：缺点：低版本浏览器(ie6 ie7 ie8)不支持
#### 5）使用flex+justify-content
（1）原理、用法
>* 原理：通过CSS3中的布局利器flex中的justify-content属性来达到水平居中。
>* 用法：先将父框设置为display:flex，再设置justify-content:center。

（2）代码实例
```css
.parent {
    display:flex;
    justify-content:center;
}
<div class="parent">
    <div class="child">DEMO</div>
</div>
```
（3）优缺点
>* 优点：设置parent即可
>* 缺点：低版本浏览器(ie6 ie7 ie8)不支持

### 垂直居中
#### 1）使用table-cell+vertical-align

（1）原理、用法
>* 原理：通过将父框转化为一个表格单元格显示（类似 <td> 和 <th>），再通过设置属性，使表格单元格内容垂直居中以达到垂直居中。
>* 用法：先将父框设置为display:table-cell，再设置vertical-align:middle。

（2）代码实例
```css
.parent {
    display:table-cell;
    vertical-align:middle;
}
<div class="parent">
    <div class="child">DEMO</div>
</div>
```
（3）优缺点
>* 优点：兼容性较好，ie8以上均支持
#### 2）使用absolute+transform

（1）原理、用法
>* 原理：类似于水平居中时的absolute+transform原理。将子框设置为绝对定位，移动子框，使子框上边距离相对框上边边框的距离为相对框高度的一半，再通过向上移动子框的一半高度以达到垂直居中。当然，在此之前，我们需要设置父框为相对定位，使父框成为子框的相对框。
>* 用法：先将父框设置为position:relative，再设置子框position:absolute，top:50%，transform:translateY(-50%)。

2）代码实例
```css
.parent {
    position: relative;
}

.child {
    position: absolute;
    top: 50 %;
    transform: translateY(- 50 %);
}
<div class="parent">
    <div class="child">DEMO</div>
</div>
```
（3）优缺点
>* 优点：居中元素不会对其他的产生影响
>* 缺点：transform属于css3内容，兼容性存在一定问题，高版本浏览器需要添加一些前缀

#### 3）使用flex+align-items
（1）原理、用法
>* 原理：通过设置CSS3中的布局利器flex中的属性align-times，使子框垂直居中。
>* 用法：先将父框设置为position:flex，再设置align-items:center。

（2）代码实例
```css
.parent {
  display:flex;
  justify-content:center;
}
<div class="parent">
    <div class="child">DEMO</div>
</div>
```
（3）优缺点
>* 优点：只设置parent
>* 缺点：兼容性存在一定问题


### 水平垂直居中
#### 1）使用absolute+transform
（1）原理、用法
>* 原理：将水平居中时的absolute+transform和垂直居中时的absolute+transform相结合。详见：水平居中的3）和垂直居中的2）。
>* 见水平居中的3）和垂直居中的2）。

（2）代码实例
```css
.parent {
    position: relative;
}
.child {
    position: absolute;
    left: 50 %;
    top: 50 %;
    transform: tranplate(- 50 %, - 50 %);
}
    <div class="parent">
        <div class="child">
            DEMO
        </div>
    </div>
```
（3）优缺点
>* 优点：child元素不会对其他元素产生影响
>* 缺点：兼容性存在一定问题

#### 2）使用inline-block+text-align+table-cell+vertical-align
（1）原理、用法
>* 原理：使用inline-block+text-align水平居中，再用table-cell+vertical-align垂直居中，将二者结合起来。详见：水平居中的1）和垂直居中的1）。
>* 见水平居中的1）和垂直居中的1）。

（2）代码实例
```css
.parent {
    text-align: center;
    display: table-cell;
    vertical-align: middle;
}

.child {
    display: inline -block;
}
    <div class="parent">
        <div class="child">
            DEMO
        </div>
    </div>
```
（3）优缺点
>* 优点：兼容性较好

#### 3）使用flex+justify-content+align-items
（1）原理、用法
>* 原理：通过设置CSS3布局利器flex中的justify-content和align-items，从而达到水平垂直居中。详见：水平居中的4）和垂直居中的3）。
>* 见水平居中的4）和垂直居中的3）。

（2）代码实例
```css
.parent {
    display:flex;
    justify-content:center;
    align-items:center;
}
<div class="parent">
        <div class="child">
            DEMO
        </div>
</div>
```
（3）优缺点
>* 优点：只设置了parent
>* 缺点：兼容性存在一定问题
