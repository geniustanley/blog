---
title: UVa 11236 - Grocery store
date: 2017-02-15 19:54:57
banner: https://i.imgur.com/rR7ED24.png 
tags:
  - UVa
---

枚舉前三個價錢, 第四個價錢用算的

<!--more-->

[11236 - Grocery store](https://uva.onlinejudge.org/external/112/11236.pdf)

## 解法

因為不想要浮點數所以我們把全部數字乘以 100 變成整數

原本的平衡式 :
``a + b + c + d = a * b * c * d``

變成整數的平衡式 :
``100(a + b + c + d) * 1000000 = 100a * 100b * 100c * 100d``

把平衡式的變數換成我們用的整數
100a = A
100b = B
100c = C
100d = D

``(A + B + C + D) * 1000000 = A * B * C * D``

``(A + B + C) * 1000000 = A * B * C * D - 1000000D``

``(A + B + C) * 1000000 = D * (A * B * C - 1000000)``

``D = (A + B + C) * 1000000 / (A * B * C - 1000000)``

p.s. ``(A * B * C - 1000000)`` 可以拿來剪枝

## code

``` c++
#include <stdio.h>
#include <math.h>
int main(void)
{
  int d, p, s;
  for (int a = 0; a+a+a+a <= 2000; a++)
    for (int b = a; a+b+b+b <= 2000; b++)
      for (int c = b; a+b+c+c <= 2000; c++) {
        p = (long long)a*b*c;
        if (p <= 1000000) continue;
        s = (a+b+c);
        if (s*1000000 % (p - 1000000)) continue;
        d = s*1000000 / (p - 1000000);
        if (a+b+c+d > 2000 || d < c) continue;
        printf("%d.%02d %d.%02d %d.%02d %d.%02d\n", a/100, a%100, b/100, b%100, c/100, c%100, d/100, d%100);
      }

  return 0;
}
```

reference: [morris](https://github.com/morris821028/UVa/blob/master/volume112/11236%20-%20Grocery%20store.cpp)

