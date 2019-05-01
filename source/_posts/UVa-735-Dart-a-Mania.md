---
title: UVa 735 - Dart-a-Mania
date: 2017-02-08 04:36:14
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

試試看 tuple + set，好用

<!--more-->

[735 - Dart-a-Mania](https://uva.onlinejudge.org/external/7/735.pdf)

## 解法

第一個飛鏢的所有可能得分 0 ~ 20 * ( 1 | 2 | 3 )

第二個飛鏢的所有可能得分 0 ~ 20 * ( 1 | 2 | 3 )

第三個飛鏢的所有可能得分 0 ~ 20 * ( 1 | 2 | 3 )

上面三個 set 拿去枚舉就可以了

combinations 可以用 tuple + set 爽算

## code

``` c++
#include <stdio.h>
#include <set>
#include <tuple>
#include <algorithm>
using namespace std;
int main(void)
{
  int n, permutations;
  int tmp[3];

  set<int> s1, s2, s3;
  set<int>::iterator i1, i2, i3;

  for (int i = 0; i <= 20; i++)
    for (int j = 1; j <= 3; j++) {
      s1.insert(i*j); // 把第一次飛鏢的得分全記下來
      s2.insert(i*j); //   第二次
      s3.insert(i*j); //   第三次
    }
  s1.insert(50); // BULLS EYE 50 分
  s2.insert(50);
  s3.insert(50);


  while (EOF != scanf("%d", &n) && n > 0) {

    set<tuple<int, int, int> > combinations;
    permutations = 0;

    for (i1 = s1.begin(); i1 != s1.end(); i1++)
      for (i2 = s2.begin(); i2 != s2.end(); i2++)
        for (i3 = s3.begin(); i3 != s3.end(); i3++)
          if (*i1 + *i2 + *i3 == n) { // 枚舉成功
            permutations++; // 某種飛鏢組合成功了
            tmp[0] = *i1, tmp[1] = *i2, tmp[2] = *i3; 
            sort(tmp, tmp+3); // sort 一下 tuple 順序才會對
            combinations.insert(tuple<int, int, int> (tmp[0], tmp[1], tmp[2]));
          }

    if (combinations.size()) {
      printf("NUMBER OF COMBINATIONS THAT SCORES %d IS %d.\n", n, combinations.size());
      printf("NUMBER OF PERMUTATIONS THAT SCORES %d IS %d.\n", n, permutations);
    } else {
      printf("THE SCORE OF %d CANNOT BE MADE WITH THREE DARTS.\n", n);
    }


    printf("**********************************************************************");
    puts("");
  }

  printf("END OF OUTPUT\n");

  return 0;
}
```

