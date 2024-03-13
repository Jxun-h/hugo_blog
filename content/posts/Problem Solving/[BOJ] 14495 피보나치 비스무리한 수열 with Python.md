---
author: ["Jxun-h"]
title: "[BOJ] 14495 피보나치 비스무리한 수열 with Python"
date: "2022-07-17 01:39:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/14495" target="_blank">BOJ 14495 피보나치 비스무리한 수열</a>

<br>

### 💡 조건

1.  피보나치 비스무리한 수열은 f(n) = f(n-1) + f(n-3)인 수열이다.  
    f(1) = f(2) = f(3) = 1이며 피보나치 비스무리한 수열을 나열하면 다음과 같다.

2.  자연수 n을 입력받아 n번째 피보나치 비스무리한 수열을 구하는 문제.

3.  자연수 n의 범위는 (1 ≤ n ≤ 116) 이다.

4.  **DP** 유형의 문제

<br>

## 🔖 예제 및 실행결과

#### 예제

```py
10
```

#### 실행결과

```py
19
```

<br>

## ⌨️ 문제 풀이

1.  문제에 점화식이 주어졌다.

<br>

## 🖥 소스 코드

```py
from sys import stdin

dp = [0 for _ in range(120)]
dp[0:3] = [1, 1, 1, 2]

for x in range(4, 117):
    dp[x] = (dp[x - 3] + dp[x - 1])

print(dp[int(stdin.readline()) - 1])
```
