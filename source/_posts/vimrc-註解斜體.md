---
title: .vimrc 註解斜體
date: 2017-03-21 22:21:44
banner: https://i.imgur.com/kvZYkZ6.png
tags:
  - linux
---

vim 註解斜體設定

<!--more-->

一切開始之前有個很 **嚴重** 的問題

## 為什麼註解要 *斜體*  ?

***# 註解寫斜體就是潮阿***

``.vimrc`` 註解要 ***斜體*** 可以輕鬆設定下面這行

## ``highlight Comment cterm=italic``

但是！

## 會失敗

因為 ``colorscheme`` 會把這個設定蓋掉

所以一定要先設定下面這行

``colorscheme default``


## 所以

``.vimrc`` 裡面要兩行

``` .vimrc
colorscheme default
highlight Comment cterm=italic
```



