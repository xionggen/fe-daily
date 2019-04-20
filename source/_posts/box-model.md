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

#### 4.边距重叠（BFC）解决方案
todo...
