---
title: UVa 10474 - Where is the Marble?
date: 2017-12-08 01:21:47
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

水題

<!--more-->

[UVA 10474 - Where is the Marble?](https://uva.onlinejudge.org/external/104/10474.pdf)

## code

``` c++
#include <stdio.h>
#include <algorithm>
using namespace std;
int main(void)
{
  int N, Q;
  int x, y[10005];
  int c = 0;

  while (EOF != scanf("%d %d", &N, &Q) && (N || Q)) {
    printf("CASE# %d:\n", ++c);
    for (int i = 0; i < N; i++) {
      scanf("%d", &y[i]);
    }
    sort(y, y+N);

    for (int i = 0; i < Q; i++) {
      scanf("%d", &x);
      int found = 0;
      for (int j = 0; j < N; j++) {
        if (y[j] == x) {
          printf("%d found at %d\n", x, j+1);
          found = 1;
          break;
        }
      }
      if (!found) {
        printf("%d not found\n", x);
      }
    }
  }

  return 0;
}
```

