---
title: UVa 416 - LED Test
date: 2017-02-26 01:19:45
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

雖然這題是 Recursive Backtracking，但是我覺得狀態壓縮的技巧比較像重點

<!--more-->

[416 - LED Test](https://uva.onlinejudge.org/external/4/416.pdf)

## 解法

1. 把 7 段顯示器的燈號換成用 binary 加總來存
2. 把每個可能的 `` count down sequence `` 都嘗試過一次 ( 最多 10 次 )
3. 把每次可能壞掉的燈號都嘗試過一次 ( 最多 2^7 = 127 種壞法 )

## code

``` c++
#include <stdio.h>
#include <string.h>
#include <math.h>
char table[10][7] = {
  {'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'N'},
  {'N', 'Y', 'Y', 'N', 'N', 'N', 'N'},
  {'Y', 'Y', 'N', 'Y', 'Y', 'N', 'Y'},
  {'Y', 'Y', 'Y', 'Y', 'N', 'N', 'Y'},
  {'N', 'Y', 'Y', 'N', 'N', 'Y', 'Y'},
  {'Y', 'N', 'Y', 'Y', 'N', 'Y', 'Y'},
  {'Y', 'N', 'Y', 'Y', 'Y', 'Y', 'Y'},
  {'Y', 'Y', 'Y', 'N', 'N', 'N', 'N'},
  {'Y', 'Y', 'Y', 'Y', 'Y', 'Y', 'Y'},
  {'Y', 'Y', 'Y', 'Y', 'N', 'Y', 'Y'},
};
int LED[10];
int inputs[10];
char s[10];

bool dfs(int v, int n, int maxx) {
  if (n < 0) {
    return true;
  }

  for (int i = 0; i <= maxx; i++) {
    // i 是 maxx 壞掉燈管的一部分， LED & 壞掉 == inputs
    if ((i&maxx) == i && (LED[v]&i) == inputs[n])
      if (dfs(v-1, n-1, i))
        return true;
  }
  return false;
}

int main(void)
{
  int N;
  int match;

  memset(LED, 0, sizeof(LED));

  for (int i = 0; i < 10; i++)
    for (int j = 0; j < 7; j++)
      if (table[i][j] == 'Y')
        LED[i] += (int)pow(2, j);


  while (EOF != scanf("%d", &N) && N) {

    match = 0;

    memset(inputs, 0, sizeof(inputs));
    for (int i = N-1; i >= 0; i--) {
      scanf(" %s", s);
      for (int j = 0; j < 7; j++) { 
        if (s[j] == 'Y')
          inputs[i] += (int)pow(2, j);
      }
    }

    for (int i = N-1; i < 10; i++)
      if (dfs(i, N-1, 127)) {
        match = 1;
        break;
      }

    if (match) printf("MATCH");
    else printf("MISMATCH");
    puts("");
  }

  return 0;
}
```

