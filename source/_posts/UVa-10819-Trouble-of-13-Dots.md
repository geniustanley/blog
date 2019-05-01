---
title: UVa 10819 - Trouble of 13-Dots
date: 2017-12-12 19:25:57
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

0-1 knapsack

<!--more-->

[10819 - Trouble of 13-Dots](https://uva.onlinejudge.org/external/108/10819.pdf)

## 細節

0-1 knapsack 處理完後，要檢查是否符合 refund 條件

考慮如下 input

```
1900 3
2000 5
1950 1
101  1
```

答案為 2，因為 $2000 不符合 refund 條件 ( 題目：exceeds $2000 )

解法

1. knapsack ( range: 0 ~ m+200 )
2. 如果 `1800 < m <= 2000`，則答案會出現在 `0 ~ m, 2001 ~ m+200` <br>( 以上面的例子來說，預算為 $1900，所以 13-DOT 只能花 0 ~ $1900 or $2001 ~ $2100，不能花 $2000 買 favour index = 5 的東西 )



## code

``` c++
#include <stdio.h>
#include <string.h>
#include <algorithm>
using namespace std;

int weight[105], cost[105];
int c[10220];

int main(void)
{
  int m, n;

  while (EOF != scanf("%d %d", &m, &n)) {
    for (int i = 0; i < n; i++)
      scanf("%d %d", &weight[i], &cost[i]);

    memset(c, 0, sizeof(c));
    if (m > 1800) m += 200;

    for (int i = 0; i < n; i++)
      for (int j = m; j - weight[i] >= 0; j--)
        if (c[j-weight[i]] > 0 || j == weight[i])
          c[j] = max(c[j], c[j-weight[i]]+cost[i]);


    /* 這邊寫很醜還請見諒 */
    int k = m-200;
    int ans = 0;

    if (k > 1800 && k <= 2000) {
      for (int i = 0; i < k; i++)
        ans = max(ans, c[i]);
      for (int i = 2001; i <= m; i++)
        ans = max(ans, c[i]);
    } else {
      for (int i = 0; i <= m; i++)
        ans = max(ans, c[i]);
    }
    printf("%d\n", ans);
    
  }

  return 0;
}
```
