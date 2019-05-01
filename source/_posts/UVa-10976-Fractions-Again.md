---
title: UVa 10976 - Fractions Again?!
date: 2017-02-06 07:11:09
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

明明是超簡單的數學, 亂做結果就 TLE 了

<!--more-->

[10976 - Fractions Again?!](https://uva.onlinejudge.org/external/109/10976.pdf)

## code

``` c++
#include <stdio.h>
#include <vector>
using namespace std;

int main(void)
{
  int k, x, y;
  int tmp;

  while (EOF != scanf("%d", &k)) {
    vector<pair<int, int> > v;
    vector<pair<int, int> >::iterator it;

    for (int i = k+1; i <= k*2; i++) {
      if (!((k*i) % (i-k)))
        v.push_back(pair<int, int> (k*i/(i-k), i));
    }

    printf("%d\n", v.size());

    for (it = v.begin(); it != v.end(); it++)
      printf("1/%d = 1/%d + 1/%d\n", k, it->first, it->second);
    


  }
  return 0;
}
```


