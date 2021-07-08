---
title: JS
date: 2021-03-19 08:41:29
tags: JS
---
# JS

### js 历史

![js 的历史.png](https://i.loli.net/2019/10/10/MBYG9uXqyQWPi1T.png)

### 分类

- 基本数据类型
  - number
  - string
  - boolean：a&&b，两个为真才为 true，a||b，两个为假才是 false
  - symbol (ES6 新增)
  - undefined
  - null
- 应用类型
  - object

### 区别数据类型的 api

- typeof: 不能判断 `null` 和 `函数`

- instanceof

  1. 使用范围：只能判断引用类型

  2. 原理：通过原型链

     ```javascript
     a instanceof b
     // 那么会这样比较
     //a.__proto__ === b.prototype ? 如果正确，返回 true
     //a.__proto__.__proto__ === b.prototype ? 返回 true
     // 直到 a.__proto__.__proto__ ...  === null 返回 false
     ```- Object.prototype.toString.call ([]) => 返回"[object String]"### 按值传递与按引用传递的区别，进阶版```javascript
var a = {n:1}
var b = a
a.x = a = {n: 2}
console.log (b)
console.log (a)
```重点是`a.x = a = {n: 2}` 如何处理？

1. 从左向右执行
2. 执行 a.x = a，就是让变量 a 指代的对象添加一个 x key, 并且让 x value 指向变量 a
3. 执行 a = {n: 2}

### Falsy 值

1. 0
2. NaN
3. ‘ ’
4. undfined
5. null

> JS 惯例：如果不希望别人该你的东西，就把命名改为大写：Node.ELEMENT_NODE

### JS 实践

批量删除微博脚本

```js
'use strict';
var s = document.createElement('script');
s.setAttribute('src', 'https://cdn.bootcss.com/jquery/3.4.1/jquery.min.js')
s.onload = function () {
    for (var i = 0; i < 3; i++) {
        setTimeout(function () {
            $('a[action-type="fl_menu"]')[0].click();
            $('a[title="删除此条微博"]')[0].click();
            $('a[action-type="ok"]')[0].click();
        }, 1000 * i)
    }
}
document.head.appendChild(s);
```
