---
title: UVa 10102 - The path in the colored field
date: 2017-02-09 09:57:47
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

O(N^2)

<!--more-->

[10102 - The path in the colored field](https://uva.onlinejudge.org/external/101/10102.pdf)

## code

``` c++
#include <stdio.h>
#include <math.h>
#include <vector>
using namespace std;
int main(void)
{
  int M, tmp, tmpMin, max;
  char c;

  while (EOF != scanf("%d", &M)) {
    vector<pair<int, int> > v1, v2;
    vector<pair<int, int> >::iterator it1, it2;

    for (int i = 0; i < M; i++)
      for (int j = 0; j < M; j++) {
        scanf(" %c", &c);
        if (c == '1') {
          v1.push_back(pair<int, int> (i, j));
        }
        if (c == '3') {
          v2.push_back(pair<int, int> (i, j));
        }
      }

    max = 0;
    for (it1 = v1.begin(); it1 != v1.end(); it1++) {

      tmpMin = 1e9;
      for (it2 = v2.begin(); it2 != v2.end(); it2++) {
        tmp = abs(it1->first - it2->first) + abs(it1->second - it2->second);

        if (tmp < tmpMin)
          tmpMin = tmp;
      }

      if (tmpMin > max)
        max = tmpMin;

    }
    printf("%d\n", max);
  }

  return 0;
}
```

