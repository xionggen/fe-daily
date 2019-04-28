---
title: 函数的防抖和节流
date: 2019-04-20 15:59:52
tags: javascript
---

#### 1.什么是函数的防抖和节流
* 函数的防抖
-- 当调用动作过N毫秒之后，才会执行指定的动作，如果在这N毫秒内又调用此动作则重新计算执行时间。

* 函数的节流
-- 预先设置一个执行周期，当调用动作的时间大于等于执行周期时才执行目标动作，然后进入一个新周期。

#### 2.防抖和节流有什么区别
-- 拿“坐电梯”来举例，**函数防抖**是指如果有人进入电梯，电梯预计在10s后会关门并运行，在这10s内有新的乘客进入（在指定时间内重复触发事件），电梯会从最后一个乘客进入电梯的时间开始（重新计时），重新等待10s后才会运行（触发指定动作）。而**函数节流**是指如果电梯中有一个乘客进入，会立即关门（不让其他乘客进入），等待10s后运行（执行指定动作），如果没有乘客进入，则永远不执行指定动作。

#### 3.应用场景
* 浏览器窗口的缩放事件（函数防抖）
* 拖拽事件（函数防抖）
* 文字输入事件（函数防抖）
* 移动端“加载更多”（函数节流）
...

#### 4.具体实现
* 函数防抖
```js
    /*
        fn, 动作函数
        wait, 等待时间,
        interval, 动作执行间距
    */
    function debounce(fn, wait, interval) {
        var previous = null; // 上一次运行的时间
        var timer = null;
        return function() {
            var now = +new Date();
            if(!previous) {
                previous = now;
            }
            if(now - previous > interval) { // 如果当前时间和上一次执行动作的时间的间距大于设置的动作执行间距则主动执行一次动作，防止事件一直触发但没有反馈的情况
                clearTimeout(timer);
                fn();
                previous = now;
            } else {
                clearTimeout(timer);
                timer = setTimeout(function() {
                    fn();
                }, wait);
            }
        }
    }
```

* 函数节流
```js
    function throttle(fn, wait) {
        let self = fn,
            timer,
            firstTime = false; // 记录是否是第一次执行
        return function() {
            let args = arguments,
                me = this;
            if(firstTime) {
                self.apply(me, args);
                return firstTIme = false;
            }

            if(timer) { // 如果定时器存在，表示有事件监听器在执行
                return false;
            }

            timer = setTimeout(function() {
                clearTimeout(timer);
                timer = null;
                self.apply(me, args);
            }, wait || 500)
        }
    }
```