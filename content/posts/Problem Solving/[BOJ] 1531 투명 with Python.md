---
author: ["Jxun-h"]
title: "[BOJ] 1531 투명 with Python"
date: "2022-03-12"
description: ""
summary: ""
tags: ["자료구조", "PS", "시뮬레이션", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1531" target="_blank">BOJ 1531 투명</a>

<br>

### 💡 조건

1.  세준이는 1×1크기의 그림으로 모자이크한 100×100크기의 그림을 가지고 있다.
2.  어느 날 이 모자이크 중 일부 그림이 너무 보기 싫어서 N개의 불투명한 종이로 그림을 가리기 시작했다.
3.  그림의 현재 부분 위에 M개 이하의 종이가 올려져 있으면 그림은 그 부분에서 보이게 된다.
4.  N은 0보다 크거나 같고, 50보다 작거나 같다. M은 0보다 크거나 같고, 50보다 작거나 같다.
5.  왼쪽 아래 모서리의 x, y좌표, 오른쪽 위 모서리의 x, y좌표 순으로 주어진다.  
    모든 좌표는 100보다 작거나 같은 자연수이다.
6.  **시뮬레이션, 구현**

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3 1
21 21 80 80
41 41 60 60
71 71 90 90
```

#### 실행결과

```py
500
```

<br>

### ⌨️ 문제 풀이

1.  N개의 불투명한 종이의 좌표를 받아서 x1부터 x2까지, y1부터 y2까지 순회한다.
2.  순회하면서 해당하는 인덱스에 해당하는 배열의 값이 False라면 1로 변경한다.
3.  순회하면서 해당하는 인덱스에 해당하는 배열의 값이 False가 아니라면 + 1 해준다.
4.  100 * 100 크기의 좌표를 순회하면서 m 이상의 크기가 있다면 res + 1 해준다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

board = [[False] * 101 for _ in range(101)]
n, m = map(int, stdin.readline().split())

for _ in range(n):
    x1, y1, x2, y2 = map(int, stdin.readline().split())

    for i in range(x1, x2 + 1):
        for j in range(y1, y2 + 1):
            if board[i][j] is False:
                board[i][j] = 1
            else:
                board[i][j] += 1

res = 0
for i in range(1, 101):
    for j in range(1, 101):
        if board[i][j] > m:
            res += 1

print(res)
```

<br>

### 💾 느낀점