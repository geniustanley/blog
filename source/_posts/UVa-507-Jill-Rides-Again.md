---
title: UVa 507 - Jill Rides Again
date: 2017-12-25 23:47:42
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

[507 - Jill Rides Again](https://uva.onlinejudge.org/external/5/507.pdf)

## Solution

Maximum Subarray

Be careful of the problem description
> If more than one segment is maximally nice, choose the one with the longest cycle ride (largest j − i). 
To break ties in longest maximal segments, choose the segment that begins with the earliest stop (lowest i).

Carefully set your condition

`(sum > mx || (sum == mx && i+1-start > final_end - final_start)`



## code

``` c++
#include <stdio.h>
int main(void)
{
  int b, s, n;
  int mx;
  int start, final_start, final_end;
  int sum;

  scanf("%d", &b);

  for (int r = 1; r <= b; r++) {
    scanf("%d", &s);

    sum = -1;
    mx = 0;
    start = -1;
    final_start = -1;
    final_end = -1;

    for (int i = 1; i < s; i++) {
      scanf("%d", &n);

      if (sum >= 0) sum += n;
      else {
        sum = n;
        start = i;
      }

      if (sum > mx || (sum == mx && i+1-start > final_end - final_start)) {
        mx = sum;
        final_end = i+1;
        final_start = start;
      }
    }
    
    if (mx == 0)
      printf("Route %d has no nice parts\n", r);
    else
      printf("The nicest part of route %d is between stops %d and %d\n", r, final_start, final_end);


  }
  
  return 0;
}
```
