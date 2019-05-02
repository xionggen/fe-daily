---
title: 闭包的学习和理解
date: 2019-04-20 15:55:00
tags: [javascript, js]
---

#### 1.什么是闭包

闭包是指有权访问另一个函数作用域中的变量的函数，也就是说，闭包其实也是一种函数体。

#### 2.如何创建闭包

创建闭包的常见方式就是，在一个函数内部创建另一个函数，例如：

```js
    function sum (a, b) {
        return function (a, b) {
            return a + b;
        }
    }
```

#### 3.闭包的基本原理

闭包函数在创建时，外部函数会预先创建一个包含全局变量对象的作用域链并保存在内部的`[[scope]]`属性中，当调用外部函数时，会为函数创建一个执行环境，然后通过赋值函数的`[[scope]]`属性中的对象构建执行环境的作用域链。之后又会有一个活动对象（arguments对象）被创建并被推入执行环境作用域链的前端。对于外部函数的执行环境来说，其作用域链中包含两个变量对象的引用：本地活动对象（arguments对象）和全局变量对象。而此时内部函数也同样会将外部函数的活动对象添加到它自身的作用域链中，它的作用域链会被初始化为包含外部函数的活动对象和全局变量对象，因此可以直接访问外部函数中定义的变量和全局变量。

#### 4.闭包中的“陷阱”

* 一般来说，函数执行结束后，其局部活动对象就会被销毁，但是在闭包中，如果外部函数执行结束，它的局部活动对象并不会被销毁，因为此时内部函数的作用域链仍然在引用外部函数的活动对象，直到内部函数也执行结束，外部函数的活动对象才会被销毁

* 闭包只能取得外部函数中某个变量的最后一个值，因为闭包保存的是整个变量对象，而不是某个特殊的变量。例如：

```js
    function foo() {
        for(var i = 0; i < 10; i++) {
            setTimeout(function () {
                console.log(i);
            }, i * 1000)
        }
    }

    foo();
```
在示例代码中，foo()最终的结果为：会连续输出10次10，原因在于for循环定义的变量i是使用var定义的，它的作用域实际就是foo函数执行环境，setTimeout的回调函数的作用域中保存的始终的是最后一个i值（9+1=10），因此会打印是10次10，如果将代码改写成：

```js
    function func() {
        for (var i = 0; i < 10; i++) {
            setTimeout(function (j) {
                return function () {
                    console.log(j);
                }
            }(i), (i * 1000));
        }
    }
    func();
```
或者

```js
    function func() {
        for (let i = 0; i < 10; i++) {
            setTimeout(function () {
                console.log(i);
            }, (i * 1000));
        }
    }
    func();
```
就可以输出正常的结果

* 正常情况下，this对象是在运行时基于函数的执行环境绑定的，指向的是执行时的上下文环境。但是在闭包中，匿名函数的执行环境具有全局性，通常执行window，除非通过call()或者apply()改变函数的执行环境。例如：

```js
    var name = '全局变量';

    var obj = {
        name: '对象的局部变量',
        getName: function() {
            return function() {
                return this.name;
            }
        }
    }

    obj.getName()() // 输出内容为'全局变量'
```
如果想要输出对象内部的name值，可以改写成：
```js
    var name = '全局变量';

    var obj = {
        name: '对象的局部变量',
        getName: function() {
            let that = this;
            return function() {
                return that.name;
            }
        }
    }

    obj.getName()() // 输出内容为'对象局部变量'
```