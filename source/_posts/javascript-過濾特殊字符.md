---
title: javascript 過濾特殊字符
date: 2017-03-20 20:19:24
banner: https://i.imgur.com/UQeCgVS.png
tags:
  - web
---

終於把 ``og:description`` 從 ``&lt;p&gt;LIS&lt;/p&gt;`` 換成乾淨的 ``LIS`` 了

<!--more-->

大家現在看到的這個部落格是用 ``hexo`` 做的

由於 ``hexo`` 支援 ``markdown``，而且又有許多主題可以選擇

以下是簡單的運作原理

1. 藉由 [marked](https://github.com/chjj/marked) 來產生 ``markdown``
2. 用變數送給 theme
3. theme 自己用 ``html`` 以及 ``css`` 把送來的變數包起來

但是經過 [marked](https://github.com/chjj/marked) 的文字已經變成下面這樣了

``<p>你好</p>``

再經過特殊符號的轉換會變成

``&lt;p&gt;你好&lt;/p&gt;``

## 但是我 render 在 og:description 裡面就是要乾淨的 ``你好`` 阿

找了一下發現了一個很猛的寫法

## ``strip_html(字串).replace(/^\s*/, '').replace(/\s*$/, '')``

終於得到乾淨的 ``og:description``

後來經過 afg 神的提醒

## ``strip_html(字串).trim()`` 就好了

看來 regex 太爛連 code 都會變成屎

Reference: [klugjo](https://github.com/klugjo/hexo-theme-clean-blog/blob/master/layout/_partial/head.ejs)

