---
title: "Fetch 在 no-cors mode 無法設定 Content-Type: application/json"
date: 2017-03-15 20:59:00
banner: https://i.imgur.com/283wCnK.png
tags:
  - web
---

``fetch`` 在 ``no-cors`` mode 會鎖定  ``'Context-Type': 'text/plain'``

<!--more-->

昨天在接一個 ``API``，本來用 ``postman`` 都接的好好的

換了 ``fetch`` 之後，``console`` 噴了 ``Access-Control-Allow-Origin``，也就是接API的夢魘

好啦，那只能設定 ``mode: 'no-cors'``

先看 code

## code

``` javascript
fetch(url, {
  method: 'POST',
  mode: 'no-cors',
  headers: new Headers({
    'Content-Type': 'application/json',
  }),
  body: JSON.stringify(data),
}).then( (r) => (
  r.json()
)).then( (r) => {
  this.setState(r);
}).catch( (e) => {
  console.log(e);
});
```

結果怎麼送都沒辦法把資料設定成 ``application/json``

## 悲劇的 Request Headers

![Imgur](https://i.imgur.com/IOGbJrf.png)

原本我以為我的 chrome 壞掉了

翻 issue 翻了半天發現這個佛心 [回答](https://github.com/github/fetch/issues/318#issuecomment-249573195)

## ``no-cors`` 會讓 ``Content-Type`` 變成 ``immutable``

## 也就是你不能在 ``no-cors`` mode 底下修改 ``Content-Type``

## 解法：去設定 API 的 server

## 還有一件事

``fetch`` 的 ``header`` 要記得用 ``new Header()``

熱門的 [github/fetch](https://github.com/github/fetch) 裡面的範例都是直接拿 ``json`` 徒手設定，比如下面這樣，有時後會出事

``` javascript
fetch('/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    name: 'Hubot',
    login: 'hubot',
  })
})
```

## 最後再改成 async await 好爽

