---
title: Migrate from HTTP to HTTPS
date: 2017-03-12 15:25:52
banner: https://i.imgur.com/XhDQxg2.png
tags:
  - web
---

紀錄將 ``HTTP`` 轉至 ``HTTPS`` 的過程

<!--more-->

申請 ``SSL`` 憑證等等的都已經做完了，主要為把程式碼修改成 ``HTTPS``

## Infrastructure

* laravel
* react
* redux

## laravel boot

問題: 下圖的 ``static file`` 需要強制 ``HTTPS``

![Imgur](https://i.imgur.com/wn0Cs9x.png)

打開 ``app/Providers/AppServiceProvider.php`` 找到 ``boot`` function

在 function 內 append 下面的程式碼，使用  ``forceRootURL`` 強制換成 ``HTTPS``

``` php
\URL::forceRootUrl(\Config::get('app.url'));
// And this if you wanna handle https URL scheme too
// It's not usefull for http://www.example.com, it's just to make it more independant from the constant value
if (str_contains(\Config::get('app.url'), 'https://')) {
    \URL::forceScheme('https');
    //use \URL:forceSchema('https') if you use laravel < 5.4
}
```

**如果低於 laravel 5.4 記得要用 forceSchema**

## 本來想寫很多的但是好像改完了...

## 是本來寫太好嗎？

