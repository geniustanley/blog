---
title: UVa 11456 - Trainsorting
date: 2017-03-22 01:12:01
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

LIS 變形

<!--more-->

[11456 - Trainsorting](https://uva.onlinejudge.org/external/114/11456.pdf)

## 解法

把 input 中的 ``123`` 拼成一個回文 ``321 123``

然後對 ``321123`` 求 ``LIS``

題目有說 ``No two cars have the same weight`` 所以不會有重疊的狀況

## code

``` c++
#include <stdio.h>
#include <vector>
#include <algorithm>
using namespace std;
int main(void)
{
  int T, n, w;
  int train[4000];
  scanf("%d", &T);

  while (T--) {
    scanf("%d", &n);

    if (!n) {
      printf("0\n");
      continue;
    }

    vector<int> v;
    for (int i = 0; i < n; i++) {
      scanf("%d", &w);
      train[n-i-1] = train[n+i] = w;
    }

    v.push_back(train[0]);

    for (int i = 1; i < 2*n; i++) {
      if (train[i] > v.back()) {
        v.push_back(train[i]);
      } else {
        *lower_bound(v.begin(), v.end(), train[i]) = train[i];
      }
    }

    printf("%d\n", v.size());
  }

  return 0;
}
```

