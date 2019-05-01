---
title: UVa 10567 - Helping Fill Bates
date: 2017-02-24 20:56:54
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

Binary search

<!--more-->

[10567 - Helping Fill Bates](https://uva.onlinejudge.org/external/105/10567.pdf)

## 過程

1. 把 ``aaaaaaaaaaaaaabbbbbbbbbdddddddddddccccccccccccc`` 的 index 存進 vector 裡面
```
V[a] = { 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13}
V[b] = {14, 15, 16, 17, 18, 19, 20, 21, 22}
V[d] = {23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33}
V[c] = {34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46}
```
2. 對目標字串 ``abccc`` 的每一個字母都用上一個字母的 index 做 binary search
```
index = -1
index = upper_bound(V[a].begin(), V[a].end(), -1) // index = 0，因為是第一個所以用 -1, start = 0
index = upper_bound(V[b].begin(), V[b].end(), index) // index = 14
index = upper_bound(V[c].begin(), V[c].end(), index) // index = 34
index = upper_bound(V[c].begin(), V[c].end(), index) // index = 35
index = upper_bound(V[c].begin(), V[c].end(), index) // index = 36，end = 36
```

## reference

[upper_bound](http://www.cplusplus.com/reference/algorithm/upper_bound/)


## code

``` c++
#include <stdio.h>
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
int main(void)
{
  string S;
  string SS;
  int Q;
  int match, start, index;
  vector<vector<int> > v(256);
  vector<int>::iterator it;
  
  cin >> S;
  // 把每個字母的 index 都記起來
  for (int i = 0; i < S.size(); i++)
    v[S[i]].push_back(i);

  scanf("%d", &Q);

  while (Q--) {
    cin >> SS;
    match = 1;
    index = -1;
    for (int i = 0; i < SS.size(); i++) {
      it = upper_bound(v[SS[i]].begin(), v[SS[i]].end(), index);
      if (it == v[SS[i]].end()) {
        match = 0;
        break;
      }
      index = it - v[SS[i]].begin();
      index = v[SS[i]][index];
      if (!i) start = index;
    }
    if (!match) printf("Not matched\n");
    else printf("Matched %d %d\n", start, index);
  }

  return 0;
}
```

