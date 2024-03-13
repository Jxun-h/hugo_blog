---
author: ["Jxun-h"]
title: "[BOJ] 13900 순서쌍의 곱의 합 with Python"
date: "2021-12-13"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/13900" target="_blank">BOJ 13900 순서쌍의 곱의 합</a>

<br>

### 💡 조건

1.  `N`개의 정수 중 서로 다른 위치의 두 수를 뽑는 모든 경우의 두 수의 곱을 구하라.
2.  `(2 ≤ N ≤ 100,000)`  
    `N`개의 정수는 `(0 <= x <= 100000)`
3.  **수학 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
3
2 3 4
```

#### 실행결과

```python
26
```

<br>

### ⌨️ 문제 풀이

1.  숫자의 개수 `N`을 입력 받고, `N`개의 정수를 입력받아 `list` 에 저장한다.  
    결과를 출력할 `r` 이라는 변수를 생성하고, `N`개의 정수를 입력받아 저장한 `list`를 `sum()` 함수를 사용해  
    `s`에 저장한다.
2.  순서쌍의 곱은 아래와 같이 나타낼 수 있다. 만약 `a`, `b`, `c`, `d`의 숫자가 있다고 가정한다면  
    `a * b + a * c + a * d`로 나타낼 수 있다. 쉽게 표현하자면, `ab + ac + ad` 로 표현할 수 있다.
3.  2번에서 표현한 식을 **결합법칙**을 통해 묶어주게 된다면 아래와 같이 변한다.  
    `a(b+c+d)`
4.  여기서 `(b+c+d)` 는 `s-a[i]`라고 할 수 있다.  
    그래서 결국 식은 `a[i] * (s - a[i])` 과 같으며, `r`에 쭉 더해준다.
5.  여기서, `ab`는 `ba`와 같은데 표현은 저렇게 할 수 있다는 것을 기억해야한다.  
    그러므로 `r // 2`를 통해 반으로 나누어 주면 답이 출력 될 수 있다.

<br>

### 🖥 소스 코드

```python
from sys import stdin
n = int(stdin.readline())
a = list(map(int, stdin.readline().split()))
r, s = 0, sum(a)

for i in range(n):
    r += a[i] * (s - a[i])

print(r // 2)
```

<br>

### 💾 느낀점

1.  결합법칙이 중요합니다.