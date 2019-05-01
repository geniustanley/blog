---
title: UVa 12192 - Grapevine
date: 2017-02-25 04:58:46
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

Binary search

<!--more-->

[12192 - Grapevine](https://uva.onlinejudge.org/external/121/12192.pdf)

## 解法

題目：對 ``Sample 1`` 找範圍介於 ``22 90`` 的正方形
答案： 3
```
25 33 34
33 35 35
33 45 50
```

1. 先對每行做 binary search 找出上下界 ( 打叉代表不在範圍內 )
```
xx xx 25 33 34
xx xx 33 35 35
xx 33 33 45 50
23 51 66 83 xx
```
2. 由於題目規定數字 ``向右嚴格遞增`` 以及 ``向下嚴格遞增``
3. 所以正方形的 ``左上必定最小`` ``右下必定最大``
4. 所以只要從：
第一行的 ``25``
第二行的 ``33``
第三行的 ``33``
第四行的 ``23``
開始往右下角對角線延伸擴大正方形，遇到邊界 ( 撞到下面或者撞到右邊 ) 就停止
5. 其實超簡單的不要害怕


## code

``` c++
#include <stdio.h>
#include <string.h>
#include <algorithm>
#include <vector>
using namespace std;
int main(void)
{
  int N, M, Q, L, U, maxx;
  int tmp;
  int range[505][2];

  while (EOF != scanf("%d %d", &N, &M) && (N || M)) {

    vector<vector<int> > v(505);
    vector<int>::iterator lower, upper;
    for (int i = 0; i < N; i++) {
      for (int j = 0; j < M; j++) {
        scanf("%d", &tmp);
        v[i].push_back(tmp);
      }
    }

    scanf("%d", &Q);

    for (int i = 0; i < Q; i++) {
      scanf("%d %d", &L, &U);
      memset(range, 0, sizeof(range)); 
      maxx = 0;

      // 把每個 row 範圍內的值都記下來
      for (int j = 0; j < N; j++) {
        lower = lower_bound(v[j].begin(), v[j].end(), L);
        upper = upper_bound(v[j].begin(), v[j].end(), U);
        range[j][0] = lower-v[j].begin();
        range[j][1] = upper-v[j].begin();
      }

      // 每個 row 都檢查過一次
      for (int j = 0; j < N; j++) {
        int cnt = 0; // 拿該 row 範圍內第一個數字當左上角
        // 對該 row 而言正方形最大的可能性是 U - L
        for (; cnt <= range[j][1]-range[j][0]; cnt++) { 
          // 檢查對角線 ( 往右往下 ) 是否在範圍內
          if (j+cnt >= N || range[j+cnt][1] <= range[j][0]+cnt) break;
        }
        if (cnt > maxx) maxx = cnt;
      }
      printf("%d\n", maxx);
    }

    printf("-");
    puts("");
  }

  return 0;
}
```

