---
title: Functional programming 為什麼要 immutable？
date: 2017-04-01 17:08:24
banner: https://i.imgur.com/KJ7S7z2.png
tags:
  - web
---

<!--more-->

## 前言

由於硬體軟體執行效能的突破等種種原因，很久以前就已經存在的 functional programming 現在可謂大紅大紫，許多語言都紛紛開始往 functional programming 靠攏，或者提供相關函數

## 這篇文章在說什麼？

或許你有學過 functional programming 也或許沒有

不過這都不重要，我們在這篇文章中只 ``簡單舉例`` **immutable** 的好處

**只要你會很基本的 javascript，我保證每件事情都是你已經會的**

## 阿什麼是 **immutable** ？ 好處是什麼 ？

與其說一串沒人看得懂的定義說明什麼是 **immutable**，我直接做給你看，看完你就知道了

## 計算機

這是一個簡單的 ``加法乘法`` 計算機

``` javascript
var Calculator = function (n) {
  this.number = n;
};
　
Calculator.prototype.add = function (c) {
  this.number += c.number;
  return this;
};
　
Calculator.prototype.multiple = function (c) {
  this.number *= c.number;
  return this;
}
　
var a = new Calculator(4);
var b = new Calculator(2);
var c = new Calculator(0);
　
// (4 + 0) * 2 + (4 * 2) = 16
var result = a.add(c).multiple(b).add(a.multiple(b)).number;
　
console.log(result); // 32 
// 答案不對 QQ
// 因為 A 被 修改(mutate) 了
```
因為會``修改(mutate)``到物件，所以會壞掉QQ

``mutate`` 的中文是 ``變化``，但是用 ``變化`` 很詭異 = =，所以我文中的 ``修改`` 就是 ``mutate``

1. a.add(c).multiple(b) 結束的時候 a.number 被改成 8
2. a 在 a.multiple(b) 結束的時候就會被改成 8\*2 = 16
3. 最後變成 16.add(16) 變成 32

## immutable 過的計算機

感謝 [DingWeizhe](https://github.com/DingWeizhe) 提供的建議以及 [code](https://gist.github.com/DingWeizhe/babb0258639972306e76aed7f5182f84)

不直接修改並回傳 input，而``重新創造一個回傳的物件``

這次答案就是對的了

``` javascript
var Calculator = function (n) {
  this.number = n;
};
　
Calculator.prototype.add = function (c) {
  return new Calculator(this.number + c.number);
};
　
Calculator.prototype.multiple = function (c) {
  return new Calculator(this.number * c.number);
}
　
var a = new Calculator(4);
var b = new Calculator(2);
var c = new Calculator(0);
　
var result = a.add(c).multiple(b).add(a.multiple(b)).number;
　
console.log(result); // 16
```

## 再更 functional 的計算機

``` javascript
var add = function(c1, c2) { return c1 + c2; };
var multiple = function(c1, c2) { return c1 * c2; };
　
var a = 4;
var b = 2;
var c = 0;
　
var result = add(
  multiple(b, add(a, c)), multiple(a, b)
);
　
console.log(result); // 16
```

將將，答案對了，因為新版 ``coding 時不需要去紀錄目前a的狀態``

## es6 version

這邊看不懂沒關係，就是語法比較新的 javascript

``` javascript
var add = (c1, c2) => (c1 + c2);
var multiple = (c1, c2) => (c1 * c2);
　
var a = 4;
var b = 2;
var c = 0;
　
// 稍微簡化一下原本的 function
// 改成 2 * (4 + 4)
var result = multiple(b, add(a, a));
　
console.log(result); // 16
```

## 結論

上面的例子簡單說明了 **immutable** 的好處，所謂 **immutable** 就是 **不可變的**

functional 版本的計算機裡面，沒有任何一行程式碼打算去 ``修改變數`` ( 我們可以發現原版的計算機中有試圖修改變數 `` this.number += c.number `` )

當你完全不在 function 內修改變數時，你的 function 就會變成 ``pure function``，code 也會變成 ``stateless programming``

我們可以看一下 [Quora上的回答](https://www.quora.com/What-is-stateless-programming-and-what-are-some-examples)

> Stateless programming is a paradigm in which the operations (functions, methods, procedures, whatever you call them) you implement are not sensitive to the state of the computation.

## are not sensitive to the state of the computation

上述這段是原版壞掉的計算機缺少的概念

reference: [mostly-adequate-guide](https://www.gitbook.com/book/drboolean/mostly-adequate-guide)

