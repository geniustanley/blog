---
title: UVa 300 - Maya Calendar
date: 2017-03-05 17:02:48
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

<!--more-->

[300 - Maya Calendar](https://uva.onlinejudge.org/external/3/300.pdf)

## code

``` c++
#include <stdio.h>
#include <string.h>
char haab[19][10] = { "pop", "no", "zip", "zotz", "tzec", "xul", "yoxkin", "mol", "chen", "yax", "zac", "ceh", "mac", "kankin", "muan", "pax", "koyab", "cumhu", "uayet" };
char tzolkin[20][10] = { "imix", "ik", "akbal", "kan", "chicchan", "cimi", "manik", "lamat", "muluk", "ok", "chuen", "eb", "ben", "ix", "mem", "cib", "caban", "eznab", "canac", "ahau" };
int main(void)
{
  int n;
  int d, m, y; 
  int sum;
  char month[10];

  scanf("%d", &n);

  printf("%d\n", n);
  while (n--) {
    scanf(" %d. %s %d", &d, month, &y);

    for (int i = 0; i < 19; i++)
      if (!strcmp(month, haab[i])) {
        m = i;
        break;
      }

    
    sum = y*365 + m*20 + d;
    printf("%d %s %d\n", sum%260%13+1, tzolkin[sum%260%20], sum/260);
  }


  return 0;
}
```

