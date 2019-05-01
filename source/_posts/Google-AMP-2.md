---
title: Google AMP - 2
date: 2017-02-20 04:43:31
banner: https://i.imgur.com/StB17bs.png
tags:
  - Google AMP
---

AMP 成功了，[@geniusgordon](https://github.com/geniusgordon) 果然是神

<!--more-->

## 不多說，先上圖

![Imgur](https://i.imgur.com/r5FvPjR.png)

沒想到第二集就解決了，原本還以為會搞很久

不過不知道過一段時間 Google 搜尋出來會長怎麼樣，長的很悲劇我可能會來個修修改改然後發個第三集吧

是說 [@geniusgordon](https://github.com/geniusgordon) 已經有 AMP 認證了，他才剛掛上去半個小時吧= =

![Imgur](https://i.imgur.com/lq6zAPO.png)

這到底是什麼妖術

## 3 個方法產生 AMP

下面這3個方法都可以讓 Google 看懂 AMP

1. 網站直接用 AMP tag 寫
2. 用已經寫好的網站去 generate 出 AMP，要記得在原本的網站加上 ``link``，跟 Google 說明 AMP 版本的位置
3. 在 generate static web 的時候就順便 generate AMP，結果上跟方法2是一樣的，但是過程不一樣

我們今天用``方法 2``，最簡單的那種


## 步驟

1. [@geniusgordon](https://github.com/geniusgordon) 貼給我一個 repo 超神，他是用已經產生好的 static html 去 generate 出 AMP
2. 就是這個 [chiedo/gatsby-amp-starter-blog](https://github.com/chiedo/gatsby-amp-starter-blog)
3. 裡面有一個 ``ampify.js``，把整段程式碼複製下來
4. 把需要的 package 裝一裝 ``yarn add recursive-readdir cheerio image-size sync-request rimraf mkdirp node-sass``
5. 打開``ampify.js``
  A. 修改 ``inputDir`` ( 看你的 static website 放在哪裡 )
  B. 修改 ``STYLES`` 那段裡面的 ``css path``，請改成自己的 ``css path``
  C. ``amp-img`` ( 也就是 amp 世界的 ``<img>``) 會跑圖，[@geniusgordon](https://github.com/geniusgordon) 跟我說把 ``layout``改成 ``responsive`` 就會好了，這部份可以看 [文件](https://www.ampproject.org/docs/guides/responsive/control_layout)
  D. 記得在 ``<a href>`` 的那個 ``href`` 前面加上 /amp
6. 收工

## 很簡單ㄅ~~

之後再把我改好的，比較適合 hexo 的 ``ampify.js`` 放到 github 上
