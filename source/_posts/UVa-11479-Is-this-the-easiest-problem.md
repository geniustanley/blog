---
title: UVa 11479 - Is this the easiest problem?
date: 2017-12-09 13:27:19
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

水題，判斷三角形


<!--more-->

[11479 - Is this the easiest problem?](https://uva.onlinejudge.org/external/114/11479.pdf)

## 注意
1. 題目 **Each of the next T lines will contain three 32 bit signed integer.** 要用 `unsigned` 或者 `long long` 不然會錯

2. 三角形是 兩短邊相加**大於** 第三邊，所以 code 要寫 `<=` ( 我腦殘寫了 `<` 吃了一個 <span style="font-weight: bold;color: red">WA</span> )

3. 沒有等腰直角三角形

## code

``` c++
#include <stdio.h>
#include <algorithm>
using namespace std;
int main(void)
{
  int T;
  long long s[5];

  scanf("%d", &T);

  for (int i = 1; i <= T; i++) {
    printf("Case %d: ", i);
    scanf("%lld %lld %lld", &s[0], &s[1], &s[2]);
    sort(s, s+3);

    if (s[0] + s[1] <= s[2]) {
      printf("Invalid\n");
    } else if (s[0] == s[1] && s[1] == s[2]) {
      printf("Equilateral\n");
    } else if (s[0] == s[1] || s[1] == s[2]) {
      printf("Isosceles\n");
    } else {
      printf("Scalene\n");
    }
  }

  return 0;
}
```
