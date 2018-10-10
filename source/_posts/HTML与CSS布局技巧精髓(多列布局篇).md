---
title: HTML与CSS布局技巧精髓（多列布局篇）
date: 2017-12-27 20:27:00
categories: "HTML/CSS"
tags:
     - HTML/CSS
     - 布局技巧
description: HTML与CSS布局技巧精髓的居中布局
---

前端布局非常重要的一环就是页面框架的搭建，也是最基础的一环。在页面框架的搭建之中，又有居中布局、多列布局以及全局布局，今天我们就来总结总结前端干货中的CSS布局。<!--more-->


## 多列布局

### 定宽+自适应
#### 1）使用float+overflow
（1）原理、用法
> * 原理：通过将左边框脱离文本流，设置右边规定当内容溢出元素框时发生的事情以达到多列布局。
> * 用法：先将左框设置为float:left、width、margin-left，再设置实际的右框overflow:hidden。

（2）代码实例
```html
<style>
.left {
    float: left;
    width: 100px;
    margin-right: 20px;
}

.right {
    overflow: hidden;
}
</style>
<body>
    <div class="parent">
        <div class="left">
            <p>left</p>
        </div>
        <div class="right">
            <p>right</p>
            <p>right</p>
        </div>
    </div>
</body>
```
（3）优缺点
>* 优点：简单
>* 缺点：不支持ie6
#### 2）使用float+margin
（1）原理、用法
>* 原理：通过将左框脱离文本流，加上右框向右移动一定的距离，以达到视觉上的多列布局。
>* 用法：先将左框设置为float:left、margin-left，再设置右框margin-left。

（2）代码实例
```html
<style>
.left {

    float: left;
    width: 100px;
}
.right {
    margin-left: 120px;
}
</style>
<body>
    <div class="parent">
        <div class="left">
            <p>left</p>
        </div>
        <div class="right">
            <p>right</p>
            <p>right</p>
        </div>
    </div>
</body>
```
（3）优缺点：
>* 优点：简单，易理解
>* 缺点：兼容性存在一定问题，ie6下有3px的bug。right下的p清除浮动将产生bug
#### 3）使用float+margin（改良版）

（1）原理、用法
>* 原理：在1）的基础之上，通过向右框添加一个父框，再加上设置左、右父框属性使之产生BFC以去除bug。
>* 用法：先将左框设置为float:left、margin-left、position:relative，再设置右父框float:right、width:100%、margin-left，最后设置实际的右框margin-left。
（2）代码实例
```html
.<style>
.left {
    float: left;
    width: 100px;
    position: relative;
}
.right-fix {
    float: right;
    width: 100 %;
    margin-left: - 100px;
}
.right {
    margin-left: 120px;
}
</style>
<body>
    <div class="parent">
        <div class="left">
            <p>left</p>
        </div>
        <div class="right">
            <p>right</p>
            <p>right</p>
        </div>
    </div>
</body>
```
（3）优缺点
>* 优点：简单，易理解

#### 4）使用table

（1）原理、用法
>* 原理：通过将父框设置为表格，将左右边框转化为类似于同一行的td，从而达到多列布局。
>* 用法：先将父框设置为display:table、width:100%、table-layout:fixed，再设置左右框display:table-cell，最后设置左框width、padding-right。
（2）代码实例
```html
<style>
.parent {
    display: table;
    width: 100 %;
    table-layout: fixed;
}
.left {
    width: 100px;
    padding-right: 20px;
}
.right,
.left {
    display: table-cell;
}
</style>
<body>
    <div class="parent">
        <div class="left">
            <p>left</p>
        </div>
        <div class="right">
            <p>right</p>
            <p>right</p>
        </div>
    </div>
</body>
```
#### 5）使用flex
（1）原理、用法
>* 原理：通过设置CSS3布局利器flex中的flex属性以达到多列布局。。
>* 用法：先将父框设置为display:flex，再设置左框flex:1，最后设置左框width、margin-right。

（2）代码实例
```html
<style>
.parent {
    display: flex;
}
.left {
    width: 100px;
    margin-right: 20px;
}
.right {
    flex: 1;
}
</style>
<body>
    <div class="parent">
        <div class="left">
            <p>left</p>
        </div>
        <div class="right">
            <p>right</p>
            <p>right</p>
        </div>
    </div>
</body>
```
（3）优缺点
>* 优点：flex很强大
>* 缺点：兼容性存在一定问题，性能存在一定问题

### 两列定宽+一列自适应
#### 1）两列不定宽+一列自适应

（1）原理、用法
>* 原理：这个情况与一列不定宽+一列自适应查不多。
>* 用法：先将左、中框设置为float:left、margin-right，再设置右框overflow:hidden，最后给左中框中的内容设置width。

（2）代码实例
```html
<style>
.left,.center {
    float: left;
    margin-right: 20px;
}
.right {
    overflow: hidden;
}
.left p,.center p {
    width: 100px;
}
</style>
<body>
    <div class="parent">
        <div class="left">
            <p>left</p>
        </div>
        <div class="center">
            <p>center</p>
        </div>
        <div class="right">
            <p>right</p>
            <p>right</p>
        </div>
    </div>
</body>
```

### 等分布局
![](https://upload-images.jianshu.io/upload_images/10798423-3d5b6611978c8031.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/619)

>* 公式转化：
l=w*n+g*(n-1)->l=w*n+g*n-g->l+g=（w+g）*n


![](https://upload-images.jianshu.io/upload_images/10798423-4769109badf75da6.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/612)
因此，我们需要解决两个问题：

>* 如何让总宽度增加g(即：L+g)
>* 如何让每个宽包含g（即：w+g）

#### 1）使用float
（1）原理、用法
>* 原理：增大父框的实际宽度后，使用CSS3属性box-sizing进行布局的辅助。
>* 用法：先将父框设置为margin-left: -*px，再设置子框float: left、width: 25%、padding-left、box-sizing: border-box。

（2）代码实例
```html
<style>
.parent {
    margin-left: - 20px;
    //l增加g
}
.column {
    float: left;
    width: 25 %;
    padding-left: 20px;
    box-sizing: border-box;
    //包含padding区域 w+g
}
</style>
<body>
      <div class="parent">
        <div class="column"><p>1</p></div>
        <div class="column"><p>2</p></div>
        <div class="column"><p>3</p></div>
        <div class="column"><p>4</p></div>
    </div>
</body>
```
（3）优缺点
>* 优点：兼容性较好
>* 缺点：ie6 ie7百分比兼容存在一定问题

#### 2）使用table
（1）原理、用法
>* 原理：通过增加一个父框的修正框，增大其宽度，并将父框转换为table，将子框转换为tabel-cell进行布局。
>* 用法：先将父框的修正框设置为margin-left: -*px，再设置父框display: table、width:100%、table-layout: fixed，设置子框display: table-cell、padding-left。

（2）代码实例
```html
<style>
.parent-fix {
    margin-left: - 20px;
    //l+g
}
.parent {
    display: table;
    width: 100 %;
    table-layout: fixed;
}
.column {
    display: table-cell;
    padding-left: 20px;
    //w+g
}
</style>
<body>
    <div class="parent">
        <div class="column"><p>1</p></div>
        <div class="column"><p>2</p></div>
        <div class="column"><p>3</p></div>
        <div class="column"><p>4</p></div>
    </div>
</body>
```
（3）优缺点
>* 优点：结构和块数无关联
>* 缺点：增加了一层

#### 3）使用flex

（1）原理、用法
>* 原理：通过设置CSS3布局利器flex中的flex属性以达到等分布局。
>* 用法：将父框设置为display: flex，再设置子框flex: 1，最后设置子框与子框的间距margin-left。
（2）代码实例
```html
<style>
.parent {
    display: flex;
}
.column {
    flex: 1;
}
.column+.column {
    margin-left: 20px;
}
</style>
<body>
    <div class="parent">
        <div class="column"><p>1</p></div>
        <div class="column"><p>2</p></div>
        <div class="column"><p>3</p></div>
        <div class="column"><p>4</p></div>
    </div>
</body>
```
（3）优缺点
>* 优点：代码量少，与块数无关
>* 缺点：兼容性存在一定问题

### 定宽+自适应+两块高度一样高
#### 1）使用float
（1）原理、用法
>* 原理：通过过分加大左右子框的高度，辅助超出隐藏，以达到视觉上的等高。
>* 用法：将父框设置overflow: hidden，再设置左右子框padding-bottom: 9999px、margin-bottom: -9999px，最后设置左框float: left、width、margin-right，右框overflow: hidden。

（2）代码实例
```html
<style>
p {
    background: none!important;
}
.left,.right {
    background: #444;
}
.parent {
    overflow: hidden;
}
.left,.right {
    padding-bottom: 9999px;
    margin-bottom: - 9999px;
}
.left {
    float: left;
    width: 100px;
    margin-right: 20px;
}
.right {
    overflow: hidden;
}
</style>
<body>
    <div class="parent">
        <div class="left">
            <p>left</p>
        </div>
        <div class="right">
            <p>right</p>
            <p>right</p>
        </div>
    </div>
</body>
```
(3)优缺点
>* 优点：兼容性好
>* 缺点：伪等高，不是真正意义上的等高

#### 2）使用table
（1）原理、用法
>* 原理：将父框转化为tabel，将子框转化为tabel-cell布局，以达到定宽+自适应+两块高度一样高。
>* 用法：先将父框设置为display:table、width:100%、table-layout:fixed，再设置左右框为display:table-cell，最后设置左框width、padding-right。

（2）代码实例
```html
<style>
.parent {
    display: table;
    width: 100 %;
    table-layout: fixed;
}
.left {
    width: 100px;
    padding-right: 20px;
}
.right,.left {
    display: table-cell;
}
</style>
<body>
    <div class="parent">
        <div class="left">
            <p>left</p>
        </div>
        <div class="right">
            <p>right</p>
            <p>right</p>
        </div>
    </div>
</body>
```
#### 3）使用flex（1）原理、用法

>* 原理：通过设置CSS3布局利器flex中的flex属性以达到定宽+自适应+两块高度一样高。
>* 用法：将父框设置为display: flex，再设置左框width、margin-right，最后设置右框flex:1。

（2）代码实例
```html
<style>
.parent {
    display: flex;
}
.left {
    width: 100px;
    margin-right: 20px;
}
.right {
    flex: 1;
}
</style>
<body>
    <div class="parent">
        <div class="left">
            <p>left</p>
        </div>
        <div class="right">
            <p>right</p>
            <p>right</p>
        </div>
    </div>
</body>
```
（3）优缺点
>* 优点：代码少，flex很强大
>* 缺点：兼容性存在一定问题

#### 4)使用display
（1）原理、用法
>* 原理：通过设置display中的CSS3的-webkit-box属性以达到定宽+自适应+两块高度一样高。
>* 用法：将父框设置为display: -webkit-box、width: 100%，再设置左框width、margin-right，最后设置右框-webkit-box-flex: 1。

（2）代码实例
```html
<style>
.parent {
    width: 100 %;
    display: -webkit-box;
}
.left {
    width: 100px;
    margin-right: 20px;
}
.right {
    -webkit-box-flex: 1;
}
</style>
<body>
    <div class="parent">
        <div class="left">left</div>
        <div class="right">right</div>
    </div>
</body>
```
(3)优缺点
>* 缺点：兼容性存在较大的问题
