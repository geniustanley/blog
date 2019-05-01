---
title: UVa 11413 - Fill the Containers
date: 2017-02-27 15:37:12
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

Binary Search the Answer

<!--more-->

[11413 - Fill the Containers](https://uva.onlinejudge.org/external/114/11413.pdf)

感覺 ``Binary search`` 沒有寫的很漂亮，在那邊 ``+1`` ``-1`` 的，有空再重寫

## code

``` c++
#include <stdio.h>
int main(void)
{
  int n, m; 
  int c[1000005];
  int l, r, mid;
  int tmp, cnt;
  int ans;

  while (EOF != scanf("%d %d", &n, &m)) {
    l = 0;
    r = 0;
    for (int i = 0; i < n; i++) {
      scanf("%d", &c[i]);
      r += c[i];
      if (c[i] > l) l = c[i]-1;
    }

    ans = r;
    while (l < r-1) {
      mid = (l+r)/2;
      tmp = 0;
      cnt = 1;
      for (int i = 0; i < n; i++) {
        if (tmp + c[i] <= mid) {
          tmp += c[i];
        } else if (c[i] <= mid) {
          cnt++;
          tmp = c[i];
        }
      }

      if (cnt > m) {
        l = mid;
      } else {
        r = mid;
        ans = mid;
      }


    }
    printf("%d\n", ans);
  }

  return 0;
}
```

