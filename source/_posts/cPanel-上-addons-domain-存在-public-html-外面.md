---
title: cPanel 上 addons domain 存在 public_html 外面
date: 2017-03-23 23:29:27
banner: https://i.imgur.com/9esSqrc.png
tags:
  - web
---

架設多網域網站，把 ``document root`` 放在 ``public_html`` 外面的方法

<!--more-->

由於客戶要增加一個新的網站在同一台 server 上

今天當我正要把買好的 domain 設定到 server

但是！！！

遇到一個問題

## 只能把資料放在 ``public_html`` 底下

本來我已經抱持著必死的決心要把原本這樣的架構

```
public_html/A.php
public_html/B.php
public_html/C.php
public_html/D.php
public_html/E.php
```

改成

```
public_html/網站1/A.php
public_html/網站1/B.php
public_html/網站1/C.php
public_html/網站1/D.php
public_html/網站1/E.php
public_html/網站2/A.php
public_html/網站2/B.php
public_html/網站2/C.php
public_html/網站2/D.php
public_html/網站2/E.php
```

這樣會搞亂原本放在那邊的網站，而且資料超多，還有資料庫啥的，一定會死

後來竟然被我查到一個神解

[Domains: How to Host a Domain Outside of the public_html Directory](https://kb.site5.com/domains/how-to-host-a-domain-outside-of-the-public_html-directory/)

## 最重要的就是在 public_html 底下放一個 symbolic link 連到家目錄底下的乾淨資料夾

因為客戶的 server 不支援 ``ssh``，而且也沒辦法在 cpanel 裡面直接 ``ln -s``，查了一下發現大家要設定 ``symbolic link`` 都是用 ``cron job`` = =

## 步驟如下

1. 去附加網域設定新的網域連到 ``public_html/網站名稱`` ![Imgur](https://i.imgur.com/D9SSHkM.png)
2. ``cron job`` 設定 ``symbolic link`` ( 先設定每分鐘跑，設定生效再刪掉 ``cron job`` 即可 ) ![Imgur](https://i.imgur.com/ccWr1ju.png)
3. 好了，就這麼簡單 = =


是說，``cron job`` 的警告標語也太可愛了吧 ![Imgur](https://i.imgur.com/gidFkRP.png)

## ``精通``

