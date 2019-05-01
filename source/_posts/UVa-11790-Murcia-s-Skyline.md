---
title: UVa 11790 - Murcia's Skyline
date: 2017-03-25 17:36:51
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

``O(N^2)`` LIS

<!--more-->

[11790 - Murcia's Skyline](https://uva.onlinejudge.org/external/117/11790.pdf)

## 解法

一開始想的太難了

由於 ``LIS`` 是要對寬度取最大，我用 ``O(NlongL)`` 的方法結果爆了

應該一開始就用爛一點但是好寫的 ``O(N^2)`` ( 大概 3 分鐘就可以寫完了 )，如果 ``TLE`` 再想其他辦法

## code

``` c++
#include <stdio.h>
#define MAX 10005
int main(void)
{

  int T, N;
  int h[MAX], w[MAX], upper[MAX], lower[MAX];
  int increase, decrease;

  scanf("%d", &T);

  for (int t = 1; t <= T; t++) {
    scanf("%d", &N);

    increase = 0, decrease = 0;
    for (int i = 0; i < N; i++)
      scanf("%d", &h[i]);
    for (int i = 0; i < N; i++)
      scanf("%d", &w[i]);

    for (int i = 0; i < N; i++) {
      upper[i] = lower[i] = w[i];
      for (int j = 0; j < i; j++) {
        if (h[j] < h[i] && upper[i] < upper[j] + w[i]) {
          upper[i] = upper[j] + w[i];
        }
        if (h[j] > h[i] && lower[i] < lower[j] + w[i]) {
          lower[i] = lower[j] + w[i];
        }
      }
      if (upper[i] > increase) increase = upper[i];
      if (lower[i] > decrease) decrease = lower[i];

    }

    if (increase >= decrease) {
      printf("Case %d. Increasing (%d). Decreasing (%d).\n", t, increase, decrease);
    } else {
      printf("Case %d. Decreasing (%d). Increasing (%d).\n", t, decrease, increase);
    }
  }
  return 0;
}
```

reference: [小白菜又菜](http://blog.csdn.net/mobius_strip/article/details/40264311)


