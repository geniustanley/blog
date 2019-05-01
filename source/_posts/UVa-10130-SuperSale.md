---
title: UVa 10130 - SuperSale
date: 2017-12-13 14:42:12
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

0-1 knapsack

<!--more-->

[10130 - SuperSale](https://uva.onlinejudge.org/external/101/10130.pdf)

## 細節

原本看題目還以為跟台灣大賣場一樣，每卡每個商品限購一個，都寫完才發現 sample output 只是對每個家人都做一次 0-1 knapsack 超簡單Q_Q

## code

``` c++
#include <stdio.h>
#include <string.h>
#include <algorithm>
using namespace std;
int main(void)
{
  int T, N;
  int P[1005], W[1005];
  int G;
  int MW[105];
  int c[35];

  scanf("%d", &T);

  while (T--) {
    scanf("%d", &N);

    for (int i = 0; i < N; i++)
      scanf("%d %d", &P[i], &W[i]);

    scanf("%d", &G);

    for (int i = 0; i < G; i++)
      scanf("%d", &MW[i]);

    sort(MW, MW+G);


    int ans = 0;

    for (int i = 0; i < G; i++) {
      memset(c, 0, sizeof(c));

      for (int j = 0; j < N; j++) {
        for (int k = MW[i]; k >= W[j]; k--) {
          if (c[k] < c[k-W[j]] + P[j]) {
            c[k] = c[k-W[j]] + P[j];
          }
        }
      };
      ans += c[MW[i]];
    }
    printf("%d\n", ans);
    // printf("%d\n", c[MW[0]]);


  }

  return 0;
}
```
