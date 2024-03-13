---
author: ["Jxun-h"]
title: "[BOJ] 2225 합분해 with Python"
date: "2022-06-17"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2225" target="_blank">BOJ 2225 합분해</a>

<br>

### 💡 조건

1.  덧셈의 순서가 바뀐 경우는 다른 경우로 센다(1+2와 2+1은 서로 다른 경우).  
    또한 한 개의 수를 여러 번 쓸 수도 있다.

2.  첫째 줄에 두 정수 N(1 ≤ N ≤ 200), K(1 ≤ K ≤ 200)가 주어진다.

3.  첫째 줄에 답을 1,000,000,000으로 나눈 나머지를 출력한다.

4.  0부터 N까지의 정수 K개를 더해서 그 합이 N이 되는 경우의 수를 구하는 문제

5.  **DP, 다이나믹프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
20 2
```

#### 실행결과

```py
21
```

<br>

### ⌨️ 문제 풀이

1.  0부터 N까지의 정수 K개를 이용해 N을 만드는 방법은 0부터 N개까지 k-1를 만드는 개수의 합과 같다.

2.  (1) 번을 점화식으로 표현하면 아래와 같다.  
    dp[k][n] = dp[k - 1][n - l] (0 <= l <= n)

3.  (2)점화식에 따라서 n = 3, k = 3 일 경우는 아래와 같이 표현할 수 있습니다.

<br>
<center><img src='/2225.png' /></center>
<br>

4.  이 점화식을 구현했을 때 시간복잡도는 O(n * k) 로 표현할 수 있습니다.


<br>

### 🖥 소스 코드

```py
n, k = map(int, input().split())

mod = 1000000000

dp = [[0] * (n + 1) for _ in range(k + 1)]
dp[0][0] = 1

for i in range(1, k + 1):
    for j in range(n + 1):
        dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        dp[i][j] %= mod

print(dp[k][n])
```
