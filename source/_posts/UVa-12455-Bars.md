---
title: UVa 12455 - Bars
date: 2017-02-21 02:27:25
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

<!--more-->

[12455 - Bars](https://uva.onlinejudge.org/external/124/12455.pdf)

這題大概是 [uHunt](http://uhunt.felix-halim.net/id/404734) Chapter 3 照順序寫過來最水的一題

## code

``` c++
#include <stdio.h>
int n, p;
int nums[25];
int ans;

void dfs(int sum, int i) {
  if (sum > n) return ;

  if (sum == n) ans = 1;

  for (;i < p; i++) {
    dfs(sum+nums[i], i+1);
  }

}

int main(void)
{
  int t;

  scanf("%d", &t);
  while (t--) {
    scanf("%d", &n);
    scanf("%d", &p);
    for (int i = 0; i < p; i++)
      scanf("%d", &nums[i]);

    ans = 0;
    dfs(0, 0);

    if (ans) printf("YES\n");
    else printf("NO\n");
  }

  return 0;
}
```

