---
title: UVa 231 - Testing the CATCHER
date: 2017-12-14 12:24:19
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

LIS ( 其實是 LDS Longest Decreasing Subsequence ) xD

<!--more-->

[231 - Testing the CATCHER](https://uva.onlinejudge.org/external/2/231.pdf)

## code

``` c++
#include <stdio.h>
#include <algorithm>
using namespace std;

int main(void)
{
  int m[100005];
  int length[100005];
  int kase = 0;

  while (1) {

    int n = 0;

    while (scanf("%d", &m[n++])) {
      if (m[n-1] == -1) break;
    }

    if (m[0] == -1) break;

    for (int i = 0; i < 100005; i++)
      length[i] = 1;


    for (int i = 0; i < n-1; i++)
      for (int j = 0; j < i; j++)
        if (m[j] > m[i])
          length[i] = max(length[i], length[j] + 1);

    int ans = 0;
    for (int i = n-1; i >= 0; i--)
      ans = max(ans, length[i]);

    if (kase)
      puts("");

    printf("Test #%d:\n", ++kase);
    printf("  maximum possible interceptions: %d\n", ans);

  }
  
  return 0;
}
```
