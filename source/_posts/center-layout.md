---
title: 聊聊页面的水平垂直居中布局
date: 2019-04-20 15:26:21
tags: [css]
---

#### 一、使用margin: 0 auto;让元素水平居中

```html
    <div class="justify-center">haha</div>
```

```css
    .justify-center {
        width: 300px;
        marign: 0 auto;
    }
```

#### 二、使用position + margin让元素水平垂直居中

```html
    <div class="parent">
        <div class="child"></div>
    </div>
```

```css
    .parent {
        width: 500px;
        height: 300px;
        position: relative;
        background-color: aqua;
    }
    .child {
        width: 100px;
        height: 100px;
        position: absolute;
        top: 50%;
        left: 50%;
        margin-top: -50px;
        margin-left: -50px;
        background-color: blueviolet;
    }
```

#### 三、使用position + transform实现水平垂直居中;

```html
    <div class="parent">
        <div class="child"></div>
    </div>
```

```css
    .parent {
        width: 500px;
        height: 300px;
        position: relative;
        background-color: aqua;
    }
    .child {
        width: 100px;
        height: 100px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: blueviolet;
    }
```

#### 四、使用flex布局实现水平垂直居中;

```html
    <div class="parent">
        <div class="child"></div>
    </div>
```

```css
    .parent {
        width: 500px;
        height: 300px;
        display: flex;
        justify-content: center;
        align-items: center;
        background-color: aqua;
    }
    .child {
        width: 100px;
        height: 100px;
        background-color: blueviolet;
    }
```
