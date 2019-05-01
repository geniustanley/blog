---
title: UVa 1047 - Zones
date: 2017-02-19 10:33:57
banner:  https://i.imgur.com/rR7ED24.png
tags:
  - UVa
---

狀態壓縮枚舉

<!--more-->

[1047 - Zones](https://uva.onlinejudge.org/external/10/1047.pdf)

這題看到解法是什麼什麼狀態壓縮枚舉, 嚇死我了, 我也要寫上來嚇死別人

感覺狀態壓縮枚舉有點浮誇, 事實上就是枚舉而已

##  解法

1. 照順序枚舉全部的 tower 位置

2. 扣掉交集的部份 ( 狀態壓縮!? )

## 吃了兩個 WA

吃了第一個 WA 因為 ``Case Number　　%d`` 要兩格空白 ( markdown 不能顯示兩個空白, 我這邊是用兩個全形打出來的, 不要複製這段喔 )

吃了第二個 WA 因為 ``Customers`` 忘記加 ``s``

我也夠腦殘了

好險我心裡面很肯定應該不是算錯, 一定是格式問題, 所以沒花到太多白痴時間

## code

``` c++
#include <stdio.h>
#include <vector>
#include <algorithm>
#include <set>
using namespace std;
int n, b;

vector<pair<vector<int>, int> > v;
vector<pair<vector<int>, int> >::iterator it;
vector<int> ans;
vector<int> cur;
int sum;
int maxx;
int tower[25];

void dfs(int size, int index) {

  // tower 符合指定數量開始扣掉交集
  // customers 比 maxx 大就更新答案
  if (size == b) { 
    int tmpSum = sum;
    // 不要破壞答案的順序所以用 tmp 表示目前選的 tower
    vector<int> tmp = cur;
    sort(tmp.begin(), tmp.end());

    for (it = v.begin(); it < v.end(); it++) {

      // 用來存交集的 vecotor
      vector<int> inter; 

      // set_intersection 要兩個 sorted vector
      set_intersection(tmp.begin(), tmp.end(), it->first.begin(), it->first.end(), back_inserter(inter));

      if (inter.size() > 1)
        tmpSum -= (inter.size()-1)*it->second;
    }

    if (tmpSum > maxx) {
      ans = cur;
      maxx = tmpSum;
    }
  }

  // 枚舉
  
  for (;index < n; index++) {
    cur.push_back(index);
    sum += tower[index];
    dfs(size+1, index+1);
    cur.pop_back();
    sum -= tower[index];
  }

  return ;
}

int main(void)
{
  int m, t, tmp, customers;
  int cnt = 1;

  while (EOF != scanf("%d %d", &n, &b) && (n || b)) {
    v.clear();

    for (int i = 0; i < n; i++)
      scanf("%d", &tower[i]);

    scanf("%d", &m);
    while (m--) {
      scanf("%d", &t);
      vector<int> vTmp;
      for (int i = 0; i < t; i++) {
        scanf("%d", &tmp);
        vTmp.push_back(tmp-1);
      }
      sort(vTmp.begin(), vTmp.end());
      scanf("%d", &customers);
      v.push_back(pair<vector<int>, int> (vTmp, customers));
    }

    sum = 0, maxx = 0;
    dfs(0, 0);


    // output
    printf("Case Number  %d\n", cnt++);
    printf("Number of Customers: %d\n", maxx);
    printf("Locations recommended:");
    for (int i = 0; i < ans.size(); i++)
      printf(" %d", ans[i]+1);
    puts("");
    puts("");
		
  }
  return 0;
}
```

