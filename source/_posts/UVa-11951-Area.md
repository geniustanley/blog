---
title: UVa 11951 - Area
date: 2017-03-21 02:18:36
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

Max 2D Range Sum

<!--more-->

[11951 - Area](https://uva.onlinejudge.org/external/119/11951.pdf)

題目沒說 ``K`` 是殺小 = =

## 解法

這題 ``O(N^4)`` 不會過

要用 ``Maximum Sum Subarray`` 的方法，把二維壓成一維

可以看 [最大子數列問題](https://zh.wikipedia.org/wiki/%E6%9C%80%E5%A4%A7%E5%AD%90%E6%95%B0%E5%88%97%E9%97%AE%E9%A2%98)

``code`` 有點醜，我想睡惹，改天改

## code

``` c++
#include <stdio.h>
#include <string.h>
#include <algorithm>
using namespace std;

int main(void)
{
  int T;
  int N, M;
  int S;
  int pre, area;
  long long K;
  long long strips[105][105];
  long long colSum[105];
  long long sum, P;
  scanf("%d", &T);

  for (int c = 0; c < T; c++) {

    S = 0;
    P = 1e9;

    scanf("%d %d %d", &N, &M, &K);

    for (int i = 0; i < N; i++)
      for (int j = 0; j < M; j++)
        scanf("%lld", &strips[i][j]);

    for (int i = 0; i < N; i++) {
      memset(colSum, 0, sizeof(colSum));
      for (int j = i; j < N; j++) {
        for (int x = 0; x < M; x++) {
          colSum[x] += strips[j][x];
        }

        pre = 0;
        sum = 0;

        for (int x = 0; x < M; x++) {
          sum += colSum[x];

          while (sum > K)
            sum -= colSum[pre++];

          area = (j-i+1) * (x-pre+1);

          if (area > S) {
            S = area;
            P = sum;
          } else if (area == S) {
            P = min(sum, P);
          }
        }
      }
    }

    printf("Case #%d: %d %lld\n", c+1, S, P);
  }

  return 0;
}
```

