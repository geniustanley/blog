---
title: UVa 574 - Sum It Up
date: 2017-02-22 00:28:10
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

``to_string()`` 好用

<!--more-->

[574 - Sum It Up](https://uva.onlinejudge.org/external/5/574.pdf)

## code

``` c++
#include <stdio.h>
#include <iostream>
#include <vector>
#include <string>
#include <map>
using namespace std;
int t, n;
int x[12];
vector<int> v;
vector<int>::iterator it;
// 用一個 map 來紀錄，避免重複的答案
map<string, int> m;
void dfs(int sum, int i) {
  if (sum > t) return ;
  if (sum == t) {
    string tmp;
    for (it = v.begin(); it != v.end(); it++) {
      if (it != v.begin()) tmp += "+";
      tmp += to_string(*it);
    }
    if (!m[tmp]) {
      cout << tmp << endl;
      m[tmp] = 1;
    }
  }

  for (; i < n; i++) {
    v.push_back(x[i]);
    dfs(sum + x[i], i+1);
    v.pop_back();
  }
}

int main(void)
{

  while (EOF != scanf("%d %d", &t, &n) && (t || n)) {
    v.clear();
    m.clear();

    for (int i = 0; i < n; i++)
      scanf("%d", &x[i]);

    printf("Sums of %d:\n", t);
    dfs(0, 0);

    if (!m.size())
      printf("NONE\n");
  }

  return 0;
}
```

