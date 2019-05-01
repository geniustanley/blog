---
title: UVa 11553 - Grid Game
date: 2017-02-19 23:25:51
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

比八皇后簡單的八皇后

<!--more-->

[11553 - Grid Game](https://uva.onlinejudge.org/external/115/11553.pdf)

## 題目

一開始看不懂題目, 盯著 sample 看很久QQ

1. 每次 Alice 選完 row, Bob 選完 column, 會得到一個交點 ``M[i, j]``

2. 把 ``M[i, j]`` 加到 ``sum`` 裡面 ( 整場遊戲總共加 ``n`` 次 )

3. Alice 想要 ``sum`` 盡量大, Bob 想要 ``sum`` 儘量小, Alice 跟 Bob 都會用 optimally 的方式去挑選

## 解法

想成 Bob 在玩八皇后 ( row 與 column 都不衝突 ), 不過不用考慮斜的衝突的情況

其實 Alice 很可憐, 他怎麼選都不重要, 反正 Bob 就照著自己的劇本選

怎麼說呢? 我們來看 sample input 3

```
10 -5
-5 10
```

Alice 當然希望選到兩個 ``10``, 不過可憐的 Alice 完全不可能選到

一開始 Bob 用八皇后算出來自己需要 ``兩個 -5``, 所以不管 Alice 怎麼選 row, 自己只要照著自己算出來的劇本無腦選有 ``-5`` 的 column 即可

最後 Bob 就會拿到 ``-10``

## code

``` c++
#include <stdio.h>
#include <algorithm>
using namespace std;
int main(void)
{
  int t, n;
  int M[10][10];
  int p[10];
  int sum;
  int ans;

  scanf("%d", &t);

  while (t--) {
    scanf("%d", &n);

    for (int i = 0; i < n; i++)
      for (int j = 0; j < n; j++)
        scanf("%d", &M[i][j]);

    for (int i = 0; i < n; i++)
      p[i] = i;

    ans = 1e9;
    // 用 next_permutation 算八皇后
    do {
      sum = 0;
      for (int i = 0; i < n; i++) {
        sum += M[i][p[i]];
      }
      // Bob 希望盡量小, 所以 sum 變小就馬上記下來
      if (sum < ans) {
        ans = sum;
      }
    } while (next_permutation(p, p+n));

    printf("%d\n", ans);
  }

  return 0;
}
```

