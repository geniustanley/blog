---
title: UVa 10003 - Cutting Sticks
date: 2017-02-05 01:05:22
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

原本亂做結果就爆了, 這題要 dp

<!--more-->

[UVA 10003 - Cutting Sticks](https://uva.onlinejudge.org/external/100/10003.pdf)

## DP
```
cost(x, y) = min(cost(x, i) + cost(i, y) + c[y] - c[x]);
```

## 舉例
題目的 sample input 中線段長度是 100 切點是 25, 50, 75

先把前面補 0, 後面補 100 

```
c[0] | c[1] | c[2] | c[3] | c[4]
0    | 25   | 50   | 75   | 100
```

dp

```
cost(0, 4) = 
min(
  cost(0, 1) + cost(1, 4) + c[4]-c[0], // 從 c[1] = 25 切
  cost(0, 2) + cost(2, 4) + c[4]-c[0], // 從 c[2] = 50 切
  cost(0, 3) + cost(3, 4) + c[4]-c[0], // 從 c[3] = 75 切
);
```

## code

``` c++
#include <stdio.h>
#include <iostream>
using namespace std;

int l, n;
int c[55];
int dp[55][55];

int cost(int x, int y) {
  if (dp[x][y] != -1) return dp[x][y]; // 要檢查不然會 TLE
  if (!dp[x][y]) return 0; 

  dp[x][y] = 1e9;
  for (int i = x+1; i < y; i++) {
    dp[x][y] = min(dp[x][y], cost(x, i) + cost(i, y) + (c[y]-c[x]));
  }

  return dp[x][y];
}

int main(void)
{

  while (EOF != scanf("%d", &l) && l) {
    scanf("%d", &n);

    c[0] = 0;
    for (int i = 1; i <= n; i++)
      scanf("%d", &c[i]);
    c[n+1] = l;

    for (int i = 0; i <= n+1; i++)
      for (int j = 0; j <= n+1; j++) {
        if (i == j-1) dp[i][j] = 0; // 兩個連在一起的價格是 0
        else dp[i][j] = -1;
      }

    printf("The minimum cutting is %d.\n", cost(0, n+1));
  }

  return 0;
}
```
記得算過的就不要再算了不然會 TLE = =

reference: [灆洢](http://knightzone.org/?p=2572)

