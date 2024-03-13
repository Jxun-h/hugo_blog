---
author: ["Jxun-h"]
title: "[BOJ] 14916 거스름돈 with Python"
date: "2022-01-26"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "수학", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/14916" target="_blank">BOJ 14916 거스름돈</a>

<br>

### 💡 조건

1.  동전의 개수가 최소가 되도록 거슬러 주어야 한다.
2.  거스름돈 액수 n(1 ≤ n ≤ 100,000)
3.  **DP, 수학 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
13
```

#### 실행결과

```py
5
```

<br>

### ⌨️ 문제 풀이

1.  5원 동전이 몇 개 일때 최소인지 구하면 된다.
2.  int(1e9)로 결과값을 초기하화 해두고, n // 5 개부터 한개씩 5원짜리를 줄여가며 최소 갯수를 구한다.
3.  5원 개수에 해당하는 금액만큼 n에서 뺀 후, 2 로 나누어 떨어지지 않을 경우 continue
4.  5월 개수에 해당하는 금액만큼 n에서 뺀 나머지 금액이 2로 나누어 떨어지면 res 갱신

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
res = int(1e9)

for i in range(n // 5, -1, -1):
    money = n - i * 5
    cnt = i
    if money % 2 != 0:
        continue
    else:
        cnt += money // 2

    res = min(cnt, res)

print(res) if res != int(1e9) else print(-1)
```

<br>

### 💾 느낀점

1.  분류에는 DP라고 되어 있었지만, 메모이제이션은 필요가 없고, 식만 세우면 풀이가 가능한 문제였다.