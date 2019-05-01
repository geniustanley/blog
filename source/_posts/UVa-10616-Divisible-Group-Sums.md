---
title: UVa 10616 - Divisible Group Sums
date: 2017-03-28 01:53:03
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
  - '0-1Knapsack'
---

0-1 背包問題，用 DP 解

<!--more-->

[10616 - Divisible Group Sums](https://uva.onlinejudge.org/external/106/10616.pdf)

## 解法

秒殺之後吃了 ``TLE``，想半天結果還是看高手解 T_T

用 ``dp[i][j][k]`` 紀錄狀態

``i`` 代表目前選到 ``N`` 個裡面第幾個

``j`` 代表目前``選了幾個``

``k`` 代表 `` mod D `` 的值

## 狀態轉移式

``dp[i][j][k] = dp[i-1][j][k] + dp[i-1][j-1][x]``

其中 ``(x + n[i] % D) % D = k`` ( n[i] 先 mod D 的原因是因為避免超過 ``int`` 的範圍 )

``dp[i][j][k]`` 來自兩種狀態，選 ``i`` 不選 ``i``

選擇 ``i``: ``dp[i-1][j-1][x]``

不選 ``i``: ``dp[i-1][j][k]``


## code

``` c++
#include <stdio.h>
#include <string.h>
int n[205];
int N, Q;
int D, M;
int dp[205][15][25];

int solve() {

  memset(dp, 0, sizeof(dp));

  dp[0][0][0] = 1;

  for (int i = 1; i <= N; i++) {
    for (int j = 0; j <= M; j++) {
      for (int k = 0; k < D; k++) {
        // 不選 i
        dp[i][j][k] += dp[i-1][j][k];

        // 選 i
        if (j) {
          int x = (D + k - n[i-1] % D) % D; 
          dp[i][j][k] += dp[i-1][j-1][x];
        }
      }
    }
  }

  return dp[N][M][0];
}

int main(void)
{
  int c = 1;

  while (EOF != scanf("%d %d", &N, &Q) && (N || Q)) {
    printf("SET %d:\n", c++);
    for (int i = 0; i < N; i++)
      scanf("%d", &n[i]);
    for (int i = 0; i < Q; i++) {
      scanf("%d %d", &D, &M);
      printf("QUERY %d: %d\n", i+1, solve());
    }
  }

  return 0;
}
```

reference: [staginner](http://www.cnblogs.com/staginner/archive/2011/12/17/2291386.html)

