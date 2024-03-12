---
author: ["Jxun-h"]
title: "[BOJ] 1026 보물 with Python"
date: "2022-01-31"
description: ""
summary: ""
tags: ["자료구조", "PS", "정렬", "사칙연산", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1026" target="_blank">BOJ 1026 보물</a>

<br>

### 💡 조건

1.  길이가 N인 정수 배열 A와 B가 있다. 다음과 같이 함수 S를 정의하자.
2.  `S = A[0] × B[0] + ... + A[N-1] × B[N-1]`
3.  S의 값을 가장 작게 만들기 위해 A의 수를 재배열하자. 단, B에 있는 수는 재배열하면 안 된다.
4.  N은 50보다 작거나 같은 자연수이고, A와 B의 각 원소는 100보다 작거나 같은 음이 아닌 정수이다.
5.  **정렬, 사칙연산 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5
1 1 1 6 0
2 7 8 3 1
```

#### 실행결과

```py
18
```

<br>

### ⌨️ 문제 풀이

1.  가장 큰 수와 가장 작은 수를 곱하여 더하면 최솟값이 나온다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
a = sorted(list(map(int, stdin.readline().split())))
b = sorted(list(map(int, stdin.readline().split())), reverse=True)
print(sum([a * b for a, b in zip(a, b)]))
```

<br>

### 💾 느낀점

1.  정렬하여 쉽게 풀었던 문제였습니다.