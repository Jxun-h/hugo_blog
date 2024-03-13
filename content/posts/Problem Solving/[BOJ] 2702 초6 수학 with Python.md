---
author: ["Jxun-h"]
title: "[BOJ] 2702 초6 수학 with Python"
date: "2023-04-14 14:26:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "브루트포스", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2702" target="_blank">BOJ 2702 초6 수학</a>

<br>

### 💡 조건

1.  두 정수 a와 b 최소공배수는 두 수의 공통된 배수 중 가장 작은 수이고, 최대공약수는 두 수의 공통된 약수중 가장 큰 수이다.
2.  a와 b가 주어졌을 때, 최소공배수와 최대공약수를 구하는 프로그램을 작성하는 문제.
3.  첫째 줄에 테스트 케이스의 개수 T(1<=T<=1,000)가 주어진다.
4.  각 테스트 케이스는 두 정수 a와 b로 이루어져 있고, 공백으로 구분되어 있다. (1 <= a,b <= 1,000)
5.  **수학, 브루트포스** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
3
5 10
7 23
42 56
```

#### 실행결과 1

```py
10 5
161 1
168 14
```

<br>

### ⌨️ 문제 풀이

1.  math 라이브러리에 있는 lcm < 최소공배수 >, gcd <최대공약수> 함수를 사용했다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from math import gcd, lcm

for _ in range(int(stdin.readline())):
    a, b = map(int, stdin.readline().split())
    print(lcm(a, b), gcd(a, b))
```