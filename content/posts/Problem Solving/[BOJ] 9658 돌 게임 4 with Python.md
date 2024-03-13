---
author: ["Jxun-h"]
title: "[BOJ] 9658 돌 게임 4 with Python"
date: "2023-04-07 15:07:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/9658" target="_blank">BOJ 9658 돌 게임 4</a>

<br>

### 💡 조건

1.  탁자 위에 돌 N개가 있다. 상근이와 창영이는 턴을 번갈아가면서 돌을 가져가며, 돌은 1개, 3개 또는 4개 가져갈 수 있다.
2.  마지막 돌을 가져가는 사람이 게임을 지게 된다.
3.  두 사람이 **완벽하게 게임을 했을 때**, 이기는 사람을 구하는 문제.
4.  게임은 상근이가 먼저 시작한다.
5.  첫째 줄에 N이 주어진다. (1 ≤ N ≤ 1000)  
    상근이가 게임을 이기면 SK를, 창영이가 게임을 이기면 CY을 출력한다.
6.  **다이나믹 프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
6
```

#### 실행결과 1

```py
SK
```

<br>

### ⌨️ 문제 풀이

1.  돌 게임 3 와의 상황을 반대로 계산하면 된다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())

dp = [0, 0, 1, 0, 1, 1, 1, 1] + [0] * (n - 7)

for i in range(8, n + 1):
    if 0 in [dp[i - 1], dp[i - 3], dp[i - 4]]:
        dp[i] = 1
    else:
        dp[i] = 0

print("SK" if dp[n] == 1 else "CY")
```