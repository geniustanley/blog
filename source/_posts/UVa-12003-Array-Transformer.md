---
title: UVa 12003 - Array Transformer
date: 2017-02-12 17:48:58
banner: https://i.imgur.com/rR7ED24.png
tags:
  - UVa
  - 塊狀鍊表
---

塊狀鍊表

<!--more-->

[12003 - Array Transformer](https://uva.onlinejudge.org/external/120/12003.pdf)

要對一個很大的 array 做操作的時候可以用**塊狀鍊表**

>英文網路稱做 **Unrolled Linked List** ，中文網路稱作**「鬆散鏈表」**、**「塊狀鏈表」**。查無正式學術名稱。

複雜度可以去看 [演算法筆記 - Data](http://www.csie.ntnu.edu.tw/~u91029/Data.html#1)

## 舉例

以下以 sample input 舉例

1. 每塊的 size 是 sqrt(10) = 3
2. 開始分塊
```
 block1  | block2  | block3  | block4 
 1, 2, 3 | 4, 5, 6 | 7, 8, 9 | 10     
```
3. 對每塊 sort
4. query 2 ~8
	* 2, 3 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在 block1  // 有 1 參雜所以用 iterate
	* 4, 5, 6 在 block2  // binary search 
	* 7, 8 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在 block3  // 有 9 參雜所以用 iterate
5. insert
	* 找到 10 在 block4 就去修改
	* 修改完要記得 sort

> 還有要順便記位置, 就不贅述了


## code

``` c++
#include <stdio.h> 
#include <list>
#include <algorithm>
#include <math.h>
#include <vector>
using namespace std;

int size;
vector<vector<pair<int, int> > > l;

bool cmp(const pair<int, int>& a, const pair<int, int>& b) {
  return a.first < b.first;
}

int query(int L, int R, int v) {
  int lp = L/size;
  int rp = R/size;
  int sum = 0;

  vector<pair<int, int> >::iterator it;
  for (int i = lp; i <= rp; i++) { // iterate through blocks
    if (i == lp || i == rp) { // 某塊有涵蓋 L 或者 R 的話要把整塊都找過 O(sqrt(N))
      for (int j = 0; j < l[i].size(); j++) {
        if (l[i][j].first < v && l[i][j].second >= L && l[i][j].second <= R) {
          sum++;
        }
      }
    } else { // 已經 sort 好了直接 binary search 就可以了 O(log(sqrt(N)))
      // binary search 乖乖自己寫
      int left = 0, right = l[i].size()-1, middle;
      while (left < right) {
        middle = (left+right+1) / 2;
        if (l[i][middle].first < v) left = middle;
        else right = middle-1;
      }
      if (l[i][left].first >= v) left--;
      sum += left+1;
    }
  }
  return sum;
}

int main(void)
{
  int n, m, u, num, k;
  int L, R, v, p;


  while (EOF != scanf("%d %d %d", &n, &m, &u)) {

    size = (int)sqrt(n);
    vector<pair<int, int> > block;
    vector<int> ans;
    for (int i = 0, j = 1; i < n; i++) {
      scanf("%d", &num);
      ans.push_back(num); // 維護一個 ans 的 array 記答案
      block.push_back(pair<int, int> (num, i));

      if (j == size || i == n-1) {
        sort(block.begin(), block.end(), cmp);
        l.push_back(block); // 塊狀鍊表目的是幫助快速 query 跟 insert
        block.clear();
        j = 1;
      } else {
        j++;
      }
    }

    vector<pair<int, int> >::iterator it;
    while (m--) {
      scanf("%d %d %d %d", &L, &R, &v, &p);
      L--, R--, p--;
      k = query(L, R, v);

      for (it = l[p/size].begin(); it != l[p/size].end(); it++) {
        if (it->second == p) { // 找到位置一樣準備把 a[p] 換成新的
          ans[p] = (int)((long long)u*k/(R-L+1)); // 先把答案寫進 ans
          it->first = ans[p]; // 更新塊狀鍊表的值
          break;
        }
      }
      sort(l[p/size].begin(), l[p/size].end(), cmp); // 換完記得 sort
    }

    for (int i = 0; i < ans.size(); i++)
      printf("%d\n", ans[i]);

  }

  return 0;
}
```

