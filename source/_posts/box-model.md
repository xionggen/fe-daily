---
title: css盒子模型的理解与使用
date: 2019-04-19 22:16:17
tags: [css]
---

#### 1.什么是盒子模型
css的盒子模型，实际上是一种样式展示结构,html中的元素都可以通过设置margin（外边距），border（边框），padding（内边距），content（元素自身的宽度和高度）来进行盒模型样式添加。
#### 2.IE盒模型和W3C盒模型
IE盒模型是IE6以下的浏览器所遵循的，目前大部分浏览器都是遵循标准的W3C盒模型；

IE盒模型和W3C盒模型的区别在于：
* IE盒模型中元素的宽度or高度=border+padding+content;
* W3C盒模型中元素的宽度or高度=content;

#### 3.使用box-sizing优化盒模型
box-sizing是css3中新增的属性，它可以设置元素的盒模型渲染标准，属性值为：
* content-box（W3C盒模型）
* border-box（IE盒模型）
* inherit（继承自父级）

#### 4.块格式化上下文环境（BFC，Block Formatting Context）
* 什么是BFC？
-- BFC是块盒子布局过程发生的区域，它决定了元素如何对齐内容进行定位。
* BFC是如何生成的？
-- 如果元素是浮动元素（float: left/right）、绝对定位（position: absolute/fixed）、行内块（display: inline-block）、表格单元格、表格标题、overflow不为visible、display: flow-root、弹性布局（display: flex/inline-flex）、栅格布局（display: grid/inline-grid）中的任意一种，都会形成一个BFC环境
* BFC的应用场景
-- 清除元素浮动

```html
    <!--使用overflow: auto创建了一个BFC环境-->
    <div style="border: 1px solid red; overflow: auto;">
        <div style="height: 200px; float: left; border: 1px solid rebeccapurple;">我浮动了</div>
        <div style="border: 1px solid yellowgreen;">我没浮动</div>
    </div>
```
-- 创建一个新的BFC环境解决外边距重叠的问题
```html
    <div style="border: 1px solid red;">
        <div style="border: 1px solid rebeccapurple; margin: 10px 0;">我浮动了</div>
        <!--创建了一个新的BFC环境-->
        <div style="display: flow-root;">
            <div style="border: 1px solid yellowgreen; margin: 10px 0;">我没浮动</div>
        </div>
    </div>
```
创建一个新的BFC环境的方式有多种，其中**display: flow-root**会创建一个任何副作用的BFC环境，设置该属性值后，目标元素的所有内容都会参与BFC，同样也可以用来清除元素浮动的副作用。