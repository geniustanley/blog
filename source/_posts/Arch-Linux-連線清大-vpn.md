---
title: Arch Linux 連線清大 vpn
date: 2017-02-13 23:29:20
banner: https://i.imgur.com/hWQFabA.png
tags:
  - linux
---

在 Arch 裡面用 openconnect 連清大 vpn

<!--more-->

[OpenConnect](https://wiki.archlinux.org/index.php/OpenConnect)

## 步驟

1. ``packer openconnect``
2. 裝 extra/openconnect
3. 開啟瀏覽器進入清大 sslvpn 網頁 [https://sslvpn.twaren.net/nthu](https://sslvpn.twaren.net/nthu)
4. 登入
5. 開 Chrome DevTool 查看 cookie, 把 DSID 的 value 複製出來 
6. 用 openconnet + DSID 連線 ( 要記得 sudo )
```
sudo openconnect --juniper -C "DSID=從cookie拿到的DSID" https://sslvpn.twaren.net
```


## 成功!
![Imgur](https://i.imgur.com/AGshy10.png)

reference: [OPASS'S BLOG](https://opass.logdown.com/posts/303644-teaching-how-to-use-linux-login-jiaoda-vpn)

