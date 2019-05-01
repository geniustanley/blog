---
title: Google AMP - 1
date: 2017-02-20 01:25:53
banner: https://i.imgur.com/StB17bs.png
tags:
  - Google AMP
---

忘了今天在哪個社團看到有人問 AMP，有點興趣就去查了一下

<!--more-->


## AMP 全名
> Accelerated Mobile Pages

假如有 AMP 的話用手機搜尋時 Google 搜尋出來的結果會潮潮的有一個閃電，據說頁面載入速度會快四倍

![Imgur](https://i.imgur.com/Y7JSzpU.png)

## 怎麼知道我的網站有沒有 AMP

基本上你不做就是沒有

不知道以後 ( 今天是 2017/02/20 ) 的各家 framework 會不會直接支援，不過 ``WordPress`` 很方便的裝個 ``plugin`` 就可以有 AMP 了

如果想要測試可以在 Google 官方的 [AMP 測試](https://search.google.com/search-console/amp) 測試網站的 AMP 程度

我得到了一堆慘不忍睹的紅色

![Imgur](https://i.imgur.com/t6Fqtof.png)

是說我的 ``github.io`` 的載入速度已經讓我很滿意了

[Mobile Website Speed Testing Tool - Google](https://testmysite.thinkwithgoogle.com/) 又是完美的 ``100%``，所以我一開始也沒有很想要用 AMP

![Imgur](https://i.imgur.com/hx2AVW7.png)

我想說先問問看 [@geniusgordon](https://github.com/geniusgordon) 有沒有用過，他說他只有聽過

後來我在想應該會對之後的 project 有幫助，還是了解一下 AMP 好了，姑且試試看先把 ``github.io`` 改造看看

於是我先跑去看了 [AMP](https://www.ampproject.org/) 

我得到一個簡單的結論

## 要有 AMP, 就要特別產生一個手機板的網站並且所有 html tag 都用 amp 規定的的 tag

Google 會特別幫你把你做好的 AMP cache 到 cdn，所以會很快，而其中的限制包括 ``js`` 會需要非同步，``css`` 會需要固定長寬

但是似乎沒有他宣稱的那麼好改阿，要引入一堆他的 ``.js`` 他才會幫我 generate amp file

於是我想說算了來看看 ``hexo`` 有沒有現成的

找到了一個日本猛人寫的 [hexo-generator-amp](https://github.com/tea3/hexo-generator-amp)

不過他的 template 不是我要的，於是 ...

## 我大概只能自己寫了

待續 ...

沒想到睡覺睡到一半還是跳起來弄好了，[Google AMP - 2](https://geniustanley.github.io/2017/02/20/Google-AMP-2/)
