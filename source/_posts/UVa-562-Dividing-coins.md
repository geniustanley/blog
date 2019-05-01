---
title: UVa 562 - Dividing coins
date: 2017-12-13 21:52:13
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

0-1 knapsack

<!--more-->

[562 - Dividing coins](https://uva.onlinejudge.org/external/5/562.pdf)

## 思路

把所有錢幣加起來除以二當作背包大小

## code

``` c++
#include <stdio.h>
#include <algorithm>
#include <string.h>
using namespace std;
int main(void)
{
  int T, m;
  int n[105];
  int dp[100005];
  int sum;

  scanf("%d", &T);

  while (T--) {
    scanf("%d", &m);

    sum = 0;
    for (int i = 0; i < m; i++) {
      scanf("%d", &n[i]);
      sum += n[i];
    }

    memset(dp, 0, sizeof(dp));
    int average = sum / 2;
    for (int i = 0; i < m; i++) {
      for (int j = average; j >= n[i]; j--) {
        dp[j] = max(dp[j], dp[j - n[i]] + n[i]);
      }
    }

    printf("%d\n", sum - dp[average] - dp[average]);
  }
  return 0;
}
```

