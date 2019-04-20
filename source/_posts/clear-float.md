---
title: 如何优雅的清除浮动
date: 2019-04-20 15:52:18
tags: css
---

#### 一、在浮动元素增加一个兄弟元素，利用clear清除浮动;

```html
    <div class="box">
        <div class="left">left-float</div>
        <div class="right">right-float</div>
        <div class="child"></div>
    </div>
```
```css
    .left {
        float: left;
    }
    .right {
        float: right;
    }
    .child {
        clear: both;
    }
```

#### 二、给父元素添加::after元素，利用clear清除浮动;
```html
    <div class="box">
        <div class="left">left-float</div>
        <div class="right">right-float</div>
    </div>
```
```css
    .left {
        float: left;
    }
    .right {
        float: right;
    }
    .box2::after {
        display: block;
        content: '';
        clear: both;
    }
```

#### 三、给父元素添加overflow属性，清除浮动;
```html
    <div class="box">
        <div class="left">left-float</div>
        <div class="right">right-float</div>
    </div>
```
```css
    .box {
        overflow: hidden;
    }
    .left {
        float: left;
    }
    .right {
        float: right;
    }
```

#### 四、将父元素也进行浮动，修改子元素浮动样式;
```html
    <div class="box">
        <div class="left">left-float</div>
        <div class="right">right-float</div>
    </div>
```
```css
    .box {
        float: left;
        width: 100%;
    }
    .left {
        float: left;
    }
    .right {
        float: right;
    }
```

#### 五、将父元素的display设置成table，清除浮动;

```html
    <div class="box">
        <div class="left">left-float</div>
        <div class="right">right-float</div>
    </div>
```
```css
    .box {
        display: table;
        width: 100%;
    }
    .left {
        float: left;
    }
    .right {
        float: right;
    }
```
