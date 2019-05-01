---
title: UVa 10576 - Y2K Accounting Bug
date: 2017-02-21 13:53:10
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

<!--more-->

[10576 - Y2K Accounting Bug](https://uva.onlinejudge.org/external/105/10576.pdf)

一開始竟然看不懂題目，沒想到竟然有公司的財務報表可以腦殘到只有兩種數字

## 題目

MS Inc. 的報表很腦殘，每個月只會有兩種數字，賺 ``s`` 或虧 ``d``

MS Inc. 每五個月的報表都是虧損，所以一年總共有 ``8``張虧損報表，1 ~ 5，2 ~ 6， ... ，7 ~ 12

## 解法

把每個月營利或虧損都試試看

2 ^ 12

## code

``` c++
#include <stdio.h>

int s, d;
int month[12];
int ans;

void dfs(int i) {

  // 從五月開始的每個月都要檢查 
  // 當月前五個月(含)的總和是否為虧損
  if (i > 4) {
    int tmp = 0;
    for (int j = i-5; j < i; j++) {
      tmp += month[j];
    }
    if (tmp >= 0) return ;
  }


  // 到年底了，可以看看整年是否營利
  // 若營利高於目前答案，就更新答案
  if (i == 12) {
    int sum = 0;
    for (int j = 0; j < 12; j++) sum += month[j];
    if (sum > ans) ans = sum;
    return ;
  }


  // 這個月營利或虧損各試一次
  month[i] = s;
  dfs(i+1);
  month[i] = -d;
  dfs(i+1);

  return ;
}

int main(void)
{

  while (EOF != scanf("%d %d", &s, &d)) {
    ans = -1e9;
    dfs(0);

    if (ans >= 0) printf("%d\n", ans);
    else printf("Deficit\n");
  }

  return 0;
}
```

