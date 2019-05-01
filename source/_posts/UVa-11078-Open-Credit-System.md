---
title: UVa 11078 - Open Credit System
date: 2017-02-27 23:55:47
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

<!--more-->

[11078 - Open Credit System](https://uva.onlinejudge.org/external/110/11078.pdf)

## code

``` c++
#include <stdio.h>
int main(void)
{
  int T, n, tmp, Max, ans;

  scanf("%d", &T);

  while (T--) {
    scanf("%d", &n);
    ans = -1e9;
    scanf("%d", &Max);
    for (int i = 1; i < n; i++) {
      scanf("%d", &tmp);
      if (Max - tmp > ans) ans = Max - tmp;
      if (tmp > Max) Max = tmp;
    }
    printf("%d\n", ans);
  }

  return 0;
}
```

