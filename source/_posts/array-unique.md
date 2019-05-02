---
title: 数组去重的多种实现方式
date: 2019-04-20 15:21:26
tags: [javascript, js]
---

方法一：定义一个新数组，遍历目标数组，使用indexOf判断目标数组的元素是否在新数组中存在，如果不存在就把元素放入到新数组中

```js
    function unique(arr) {
        let res = [];
        arr.forEach(ele => {
            res.indexOf(ele) === -1 && res.push(ele);
        })
        return res;
    }
```

方法二：定义一个新数组，遍历目标数组，使用indexOf判断当前元素第一次出现的位置是否和当前的位置一致，如果一致就放入到新数组中

```js
    function unique(arr) {
        let res = [];
        arr.forEach((ele, idx) => {
            arr.indexOf(ele) === idx && res.push(ele);
        })
        return res;
    }
```

方法三：使用Set结构的唯一性

```js
    function unique(arr) {
        return Array.from(new Set(arr));
    }
```

方法四：利用对象键的唯一性

```js
    function unique(arr) {
        let obj = {};
        let res = [];
        arr.forEach(ele => {
            if (!obj[ele]) {
                obj[ele] = true;
                res.push(ele);
            }
        })
        return res;
    }
```

方法五：先将数组排序，遍历数组，如果当前元素和前一位元素或者后一位元素相同，则删除当前元素

```js
    function unique(arr) {
        for (let i = 1; i < arr.length - 1; i++) {
            if (arr[i] === arr[i - 1] || arr[i] === arr[i + 1]) {
                arr.splice(arr[i]);
            }
        }
        return arr;
    }
```