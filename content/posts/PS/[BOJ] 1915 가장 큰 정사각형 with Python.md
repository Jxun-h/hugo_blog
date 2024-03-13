---
author: ["Jxun-h"]
title: "[BOJ] 1915 가장 큰 정사각형 with Python"
date: "2022-06-14"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1915" target="_blank">BOJ 1915 가장 큰 정사각형</a>

<br>

### 💡 조건

1.  아래와 같은 예제에서는 가운데의 2×2 배열이 가장 큰 정사각형이다.  

<br>
<center><img src='/1915.png' width="318" /></center>
<br>

2.  첫째 줄에 n, m(1 ≤ n, m ≤ 1,000)이 주어진다.  
    다음 n개의 줄에는 m개의 숫자로 배열이 주어진다.

3.  n×m의 0, 1로 된 배열이 있다. 이 배열에서 1로 된 가장 큰 정사각형의 크기를 구하는 문제.

4.  **DP, 다이나믹프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4 4
0100
0111
1110
0010
```

#### 실행결과

```py
4
```

<br>

### ⌨️ 문제 풀이

1.  가장 큰 정사각형의 넓이를 구해야하는데, 정사각형이 되는 상태를 dp 배열에 저장하면서 가장 큰 변의 길이를 구하면 된다.

2.  한 칸도 정사각형이 될 수 있기에, 최소 넓이의 값은 1이다.

3.  현재 순회하고 있는 좌표 x, y 를 기준으로 x-1, y-1 이 1일 때  
    dp 리스트의 현재 순회하는 좌표 x, y를 기준으로 왼쪽, 위, 왼쪽 대각선을 살펴보고 가장 작은 값 + 1을 구해  
    dp[x][y]에 저장하고, 이 값을 ans 값과 비교하여 가장 큰 값으로 갱신한다.

4.  리스트를 모두 순회했다면, 저장된 ans 값을 제곱하여 넓이를 구하고 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = map(int, stdin.readline().split())
arr = []
for _ in range(n):
    arr.append(list(map(int, list(stdin.readline().rstrip()))))

ans = 0
dp = [[0] * (m + 1) for _ in range(n + 1)]

for i in range(1, n + 1):
    for j in range(1, m + 1):
        if arr[i - 1][j - 1] == 1:
            dp[i][j] = min(dp[i][j - 1], dp[i - 1][j], dp[i - 1][j - 1]) + 1
            ans = max(ans, dp[i][j])

print(ans ** 2)
```