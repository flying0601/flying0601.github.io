---
title: HTML与CSS布局技巧精髓（全屏布局篇）
date: 2018-01-27 21:27:00
categories: "HTML/CSS"
tags:
     - HTML/CSS
     - 布局技巧
description: HTML与CSS布局技巧精髓的全屏布局
---

前端布局非常重要的一环就是页面框架的搭建，也是最基础的一环。在页面框架的搭建之中，又有居中布局、多列布局以及全局布局，今天我们就来总结总结前端干货中的CSS布局。<!--more-->


## 全屏布局

### 全屏布局的特点

>* 滚动条不是全局滚动条，而是出现在内容区域里，往往是主内容区域
>* 浏览器变大时，撑满窗口
### 全屏布局的方法

![](https://upload-images.jianshu.io/upload_images/10798423-e9b52e09c0346fe6.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

#### 1）使用position
（1）原理、用法
>* 原理：将上下部分固定，中间部分使用定宽+自适应+两块高度一样高。
>* 用法：用法：见实例。

（2）代码实例
```html
<style>
html,body,.parent {
    margin: 0;
    height: 100 %;
    overflow: hidden;
}
body {
    color: white;
}
.top {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 100px;
    background: blue;
}
.left {
    position: absolute;
    left: 0;
    top: 100px;
    bottom: 50px;
    width: 200px;
    background: red;
}
.right {
    position: absolute;
    left: 200px;
    top: 100px;
    bottom: 50px;
    right: 0;
    background: pink;
    overflow: auto;
}
.right .inner {
    min-height: 1000px;
}
.bottom {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    height: 50px;
    background: black;
}
</style>
<body>
    <div class="parent">
        <div class="top">top</div>
        <div class="left">left</div>
        <div class="right">
            <div class="inner">right</div>
        </div>
        <div class="bottom">bottom</div>
    </div>
</body>
```
（3）优缺点
>* 优点：兼容性好，ie6下不支持

#### 2）使用flex
（1）原理、用法
>* 原理：通过灵活使用CSS3布局利器flex中的flex属性和flex-direction属性以达到全屏布局。
>* 用法：见实例。

（2）代码实例
```html
<style>
html,body,.parent {
    margin: 0;
    height: 100 %;
    overflow: hidden;
}
body {
    color: white;
}
.parent {
    display: flex;
    flex-direction: column;
}
.top {
    height: 100px;
    background: blue;
}
.bottom {
    height: 50px;
    background: black;
}
.middle {
    flex: 1;
    display: flex;
}
.left {
    width: 200px;
    background: red;
}
.right {
    flex: 1;
    overflow: auto;
    background: pink;
}
.right .inner {
    min-height: 1000px;
}
</style>
<body>
    <div class="parent">
        <div class="top">top</div>
        <div class="middle">
            <div class="left">left</div>
            <div class="right">
                <div class="inner">right</div>
            </div>
        </div>
        <div class="bottom">bottom</div>
    </div>
</body>
```
（3）优缺点
>* 缺点：兼容性差，ie9及ie9以下不兼容

![](https://upload-images.jianshu.io/upload_images/10798423-ec6537b225f7b2e8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)
### 全屏布局相关方案的兼容性、性能和自适应一览表
 <table width="634">        <thead style="max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">            <tr style="max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">                <th style="padding: 0.5rem 1rem;word-break: break-all;border-top-width: 1px;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;text-align: left;word-wrap: break-word !important;">方案</th>                <th style="padding: 0.5rem 1rem;word-break: break-all;border-top-width: 1px;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;text-align: left;word-wrap: break-word !important;">兼容性</th>                <th style="padding: 0.5rem 1rem;word-break: break-all;border-top-width: 1px;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;text-align: left;word-wrap: break-word !important;">性能</th>                <th style="padding: 0.5rem 1rem;word-break: break-all;border-top-width: 1px;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;text-align: left;word-wrap: break-word !important;">是否自适应</th>            </tr>        </thead>        <tbody style="max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">            <tr style="max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">Position</td>                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">好</td>                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">好</td>                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">部分自适应</td>            </tr>            <tr style="max-width: 100%;box-sizing: border-box;background-color: rgb(248, 248, 248);word-wrap: break-word !important;">                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">Flex</td>                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">较差</td>                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">差</td>                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">可自适应</td>            </tr>            <tr style="max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">Grid</td>                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">差</td>                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">较好</td>                <td style="padding: 0.5rem 1rem;word-break: break-all;border-color: rgb(233, 235, 236);max-width: 100%;box-sizing: border-box;word-wrap: break-word !important;">可自适应</td>            </tr>        </tbody>    </table>
