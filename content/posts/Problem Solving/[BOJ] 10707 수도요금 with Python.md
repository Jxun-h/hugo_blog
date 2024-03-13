---
author: ["Jxun-h"]
title: "[BOJ] 10707 수도요금 with Python"
date: "2023-04-10 17:05:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "사칙연산", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/10707" target="_blank">BOJ 10707 수도요금</a>

<br>

### 💡 조건

1.  JOI군이 살고 있는 지역에는 X사와 Y사, 두 개의 수도회사가 있다.  
    두 회사의 수도요금은 한 달간 수도의 사용량에 따라 (2)번과 같이 정해진다.
2.  X사 : 1리터당 A엔.  
    Y사 : 기본요금은 B엔이고, 사용량이 C리터 이하라면 요금은 기본요금만 청구된다.  
    용량이 C리터가 넘었을 경우 기본요금 B엔에 더해서 추가요금이 붙는다.  
    추가요금은 사용량이 C리터를 넘었을 경우 1리터를 넘었을 때마다 D엔이다.
3.  JOI군의 집에서 한 달간 쓰는 수도의 양은 P리터이다.
4.  수도요금이 최대한 싸게 되도록 수도회사를 고를 때, JOI군의 집의 1달간 수도요금을 구하여라.
5.  입력되는 정수 A,B,C,D,P는 전부 1 이상 10000 이하이다.
6.  **수학, 사칙연산** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
9
100
20
3
10
```

#### 실행결과 1

```py
90
```

#### 예제 2

```py
8
300
100
10
250
```

#### 실행결과 2

```py
1800
```

<br>

### ⌨️ 문제 풀이

1.  JOI군이 사용한 수도의 양 P 가 상한 C 보다 높다면, `min(a * p, (p - c) * d + b))`
    -   a * p : X 사 요금
    -   (p - c) * d : 상한 이상으로 사용한 수도의 양 * 추가요금
2.  JOI군이 사용한 수도의 양 P 가 상한 C 보다 낮다면, `min(a * p, b)`

<br>

### 🖥 소스 코드

```py
from sys import stdin

a, b, c, d, p = [int(stdin.readline()) for _ in range(5)]
ans = min(a * p, (p - c) * d + b) if p > c else min(a * p, b)
print(ans)
```