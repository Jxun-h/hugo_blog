---
author: ["Jxun-h"]
title: "[BOJ] 10211 Maximum Subarray with Python"
date: "2022-03-22"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/10211" target="_blank">BOJ 10211 Maximum Subarray</a>

<br>

### 💡 조건

1.  크기 N인 정수형 배열 X가 있을 때, X의 부분 배열(X의 연속한 일부분) 중  
    각 원소의 합이 가장 큰 부분 배열을 찾는 Maximum subarray problem(최대 부분배열 문제)
2.  N과 배열 X가 주어졌을 때, X의 maximum subarray의 합을 구하는 문제.
3.  배열의 크기 N이 주어진다. (1 ≤ N ≤ 1,000)
4.  배열 X의 내용을 나타내는 N개의 정수가 공백으로 구분되어 주어진다. 이때 주어지는 수는 절댓값이 1,000보다 작은 정수이다.
5.  **브루트포스 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
2
5
1 2 3 4 5
5
2 1 -2 3 -5
```

#### 실행결과

```py
15
4
```

<br>

### ⌨️ 문제 풀이

1.  i번째를 기준으로 i + 1번째 숫자부터 더했을 때, 최댓값을 구하여 res에 저장한다
2.  res 출력

<br>

### 🖥 소스 코드

```py
from sys import stdin

for _ in range(int(stdin.readline())):
    n = int(stdin.readline())
    arr = list(map(int, stdin.readline().split()))
    res = -int(1e9)
    for i in range(n):
        temp = arr[i]
        if res < temp:
            res = temp
        for j in range(i + 1, n):
            temp += arr[j]
            if temp > res:
                res = temp
    print(res)
```

<br>

### 💾 느낀점