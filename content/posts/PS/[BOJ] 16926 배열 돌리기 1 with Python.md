---
author: ["Jxun-h"]
title: "[BOJ] 16926 배열 돌리기 1 with Python"
date: "2022-05-11"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/16926" target="_blank">BOJ 16926 배열 돌리기 1</a>

<br>

### 💡 조건

1.  크기가 N×M인 배열이 있을 때, 배열을 반시계 방향으로 돌린다.
2.  첫째 줄에 배열의 크기 N, M과 수행해야 하는 회전의 수 R이 주어진다.  
    둘째 줄부터 N개의 줄에 배열 A의 원소 Aij가 주어진다.
3.  2 ≤ N, M ≤ 300  
    1 ≤ R ≤ 1,000  
    min(N, M) mod 2 = 0  
    1 ≤ Aij ≤ 108
4.  배열을 R번 회전시킨 결과를 출력하는 문제
5.  **구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5 4 7
1 2 3 4
7 8 9 10
13 14 15 16
19 20 21 22
25 26 27 28
```

#### 실행결과

```py
28 27 26 25
22 9 15 19
16 8 21 13
10 14 20 7
4 3 2 1
```

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m, r = map(int, stdin.readline().split())
arr = []
for i in range(n):
    arr.append(list(map(int, stdin.readline().split())))

for _ in range(r):
    for i in range(min(n, m) // 2):
        x, y = i, i
        value = arr[x][y]

        for j in range(i + 1, n - i):  # 좌
            x = j
            prev_value = arr[x][y]
            arr[x][y] = value
            value = prev_value

        for j in range(i + 1, m - i):  # 하
            y = j
            prev_value = arr[x][y]
            arr[x][y] = value
            value = prev_value

        for j in range(i + 1, n - i):  # 우
            x = n - j - 1
            prev_value = arr[x][y]
            arr[x][y] = value
            value = prev_value

        for j in range(i + 1, m - i):  # 상
            y = m - j - 1
            prev_value = arr[x][y]
            arr[x][y] = value
            value = prev_value

for i in arr:
    print(*i)
```
