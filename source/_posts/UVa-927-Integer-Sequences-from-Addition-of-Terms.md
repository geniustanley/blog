---
title: UVa 927 - Integer Sequences from Addition of Terms
date: 2017-02-06 04:33:33
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

<!--more-->

[927 - Integer Sequences from Addition of Terms](https://uva.onlinejudge.org/external/9/927.pdf)

## code

``` c++
#include <stdio.h>
#include <math.h>
int main(void)
{
  int t, m, d, k, n;
  long long c[30];
  long long ans;
  scanf("%d", &t);

  while (t--) {
    ans = 0;
    scanf("%d", &m);
    for (int i = 0 ; i <= m; i++)
      scanf("%lld", &c[i]);
    scanf("%d %d", &d, &k);

    for (n = 1; n*n+n < 2*k/d; n++);

    for (int i = 0; i <= m; i++)
      ans += c[i]*(long long)pow(n, i);

    printf("%lld\n", ans);
  }

  return 0;
}
```


