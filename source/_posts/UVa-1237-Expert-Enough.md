---
title: UVa 1237 - Expert Enough?
date: 2017-02-06 05:46:04
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

stl map 

<!--more-->

[1237 - Expert Enough?](https://uva.onlinejudge.org/external/12/1237.pdf)

## code

``` c++
#include <stdio.h>
#include <iostream>
#include <map>
using namespace std;
int main(void)
{
  int T, D, Q, L, H, P, multi;
  char M[100];
  string ans;
  scanf("%d", &T);

  while (T--) {
    map<string, pair<int, int> > database;
    map<string, pair<int, int> >::iterator it;

    scanf("%d", &D);

    while (D--) {
      scanf(" %s %d %d", M, &L, &H);
      string tmp = M;
      database[tmp] = pair<int, int> (L, H); 
    }

    scanf("%d", &Q);

    while (Q--) {
      scanf("%d", &P);
      multi = 0;
      ans = "";
      for (it = database.begin(); it != database.end(); it++) {
        if (P >= it->second.first && P <= it->second.second) {
          if (ans == "") {
            ans = it->first;
          } else {
            multi = 1;
            break;
          }
        }
      }

      if (multi || ans == "")
        printf("UNDETERMINED\n");
      else
        cout << ans << endl;

    }

    if (T) puts("");
  }

  return 0;
}
```


