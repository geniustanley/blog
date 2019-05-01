---
title: UVa 12032 - The Monkey and the Oiled Bamboo
date: 2017-02-27 22:18:31
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

Binary Search the Answer

<!--more-->

[12032 - The Monkey and the Oiled Bamboo](https://uva.onlinejudge.org/external/120/12032.pdf)

## code

``` c++
#include <stdio.h>
int main(void)
{
  int T, n;
  int rungs[100005];
  int l, r, m, k;
  int reach, ans;
  scanf("%d", &T);

  for (int c = 0; c < T; c++) {
    scanf("%d", &n);
    l = 0;
    r = 0;
    for (int i = 1; i <= n; i++) {
      scanf("%d", &rungs[i]);
      if (rungs[i] - rungs[i-1] > r)
        r = rungs[i] - rungs[i-1];
    }

    r += n;
    ans = r;
    while (l < r-1) {
      m = (l+r)/2;
      k = m;
      reach = 1;
      for (int i = 1; i <= n; i++) {
        if (k < (rungs[i]-rungs[i-1])) {
          reach = 0;
          break;
        }
        if (k == (rungs[i]-rungs[i-1])) k--;
      }

      if (reach) {
        r = m;
        ans = m;
      } else {
        l = m;
      }
    }

    printf("Case %d: %d\n", c+1, ans);
  }

  return 0;
}
```

