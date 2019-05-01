---
title: UVa 11517 - Exact Change
date: 2017-12-11 06:22:47
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

DP

<!--more-->

[11517 - Exact Change](https://uva.onlinejudge.org/external/115/11517.pdf)

## 心得

這題直覺想到是 DP ，否則就要 O(2^N)，但是具體作法一直沒想出來，一直朝著 0-1knapsack 的遞迴 DP 去想

最後看了 Morris 大才發現超簡單

ref: [Morris](https://github.com/morris821028/UVa/blob/master/volume115/11517%20-%20Exact%20Change.cpp)

> 稍微改了一點 我覺得 mx 那邊的優化不會快很多 但是拿掉 mx code 乾淨一些

## code

``` c++
#include <stdio.h>
int main(void)
{
  int T;
  int price;
  int n;
  int coin;

  scanf("%d", &T);

  while (T--) {
    scanf("%d", &price);
    scanf("%d", &n);

    int dp[10005] = {};
    dp[0] = 1;
    for (int i = 0; i < n; i++) {
      scanf("%d", &coin);
      for (int j = 10000; j - coin >= 0; j--) {
        if (dp[j] == 0 || dp[j] > dp[j-coin] + 1) {
          if (dp[j-coin]) {
            dp[j] = dp[j-coin] + 1;
          }
        }
      }
    }

    while (!dp[price]) price++;

    printf("%d %d\n", price, dp[price]-1);

  }
  return 0;
}
```
