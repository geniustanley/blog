---
title: Arch 與 Windows 時間互改
date: 2017-02-12 00:22:38
banner: https://i.imgur.com/K9n2bEW.png
tags:
  - linux
---

終於把時間衝突的問題解決了

<!--more-->

Arch linux 灌好之後與 Windows 之間的時間會一直互相修改, 兩邊明明都有設定 Automatic Date & Time 但是還是互相修改


這次總算處理掉了

## 爽

``` bash
sudo timedatectl --adjust-system-clock set-local-rtc true
```

