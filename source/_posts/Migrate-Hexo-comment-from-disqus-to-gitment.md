---
title: Migrate Hexo comment from disqus to gitment
date: 2017-05-23 21:35:01
banner: https://i.imgur.com/msfvYHJ.png
tags:
---

與 [Disqus](https://disqus.com/) 類似的 [多說](http://www.weibo.com/duoshuo) 即將要關閉了，許多人換到以 Github Issue 為 base 的 gitment

<!--more-->

話說 ``Github`` 章魚好可愛喔 \>////<

其實多說要關閉跟我換 gitment 沒關係，純粹是我比較喜歡 gitment

# [Gitment](https://github.com/imsun/gitment)

![Imgur](https://i.imgur.com/eihTuzi.png)

## 優點

* 用 Github Login ( 相信來看這邊逛逛的人有 Github 帳號應該多於 Disqus 帳號 )
* 支援 markdown ( 可以貼 code )
* 用 Github Issue 來管理 comment ( 我比較常上 github 以及我對 github 的愛 )
* 可以自行修改 css ( 滿喜歡 default 的設定所以我目前沒動 )
* 放一些 code 在前端就可以，不用改 server

![Imgur](https://i.imgur.com/ZWE0fBH.png)

## 缺點

* 訪客要留言要用 Github Login 然後 Authorize ( 那個 Authorize 頁面滿可怕的其實，有種當年 Facebook Authorize 在各個網站滿天飛的陰影 = = ，不過不要害怕，用力給他按下去 )
* 每發一篇文作者都需要去 initial 一下，之後訪客才能留言，因為要在 Github repo 裡面創造一個 Issue

![Imgur](https://i.imgur.com/yAs8SpA.png)

## 安裝

基本的安裝看 [Gitment](https://github.com/imsun/gitment) 的 github 就可以了，包括申請 Github OAuth，這邊主要小提一下 Hexo 部份的修改

## 開始動手改ㄅ

我用的 hexo theme 是用 [pug (jade)](https://pugjs.org/api/getting-started.html) 寫的，不會跟 html 差很多啦

找到 head 的部份，新增 css

```
link(rel="stylesheet", href=url_for("https://imsun.github.io/gitment/style/default.css"))
```

在 ``_config.yml`` 中新增剛剛申請好的資料

```
# Comment
# e.g disqus: seansun
disqus:
duoshuo:
gitment:
  owner: 你的 Github 帳號
  repo: 新建立準備放 comment 的 repo
  client_id: 剛剛申請的 client_id
  client_secret: 剛剛申請的 client_secret
```



在 comment 部份 ( 你可以 grep 一下 Disqus 放哪邊，就放他下面 ) 加上 gitment 需要的 js

```
if theme.gitment
     #gitmentContainer
     link(rel='stylesheet', href='https://imsun.github.io/gitment/style/default.css')
     script(src='https://imsun.github.io/gitment/dist/gitment.browser.js')
     script.
       var gitment = new Gitment({
         owner: '#{theme.gitment.owner}',
         repo: '#{theme.gitment.repo}',
         oauth: {
           client_id: '#{theme.gitment.client_id}',
           client_secret: '#{theme.gitment.client_secret}',
         },
       })
       gitment.render('gitmentContainer')
```

## 完成

完成後記得

``` bash
hexo clean;
hexo g;
```

## 警告

每發一篇文都要 Initial 一次，不要不小心重複 Initial，雖然不會壞掉但是會產生兩篇 Issue 有點醜，而且 Github 的 Issue 是不能刪除的，只能 Close

![Imgur](https://i.imgur.com/eihTuzi.png)

## 更新

雖然 gitment 頗帥，但 [DISQUS](https://disqus.com/) 樸素簡單還是我的愛 <3 ( 2018.01.21 )
