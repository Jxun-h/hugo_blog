---
author: ["Jxun-h"]
title: "[BOJ] 1145 적어도 대부분의 배수 with Python"
date: "2022-03-29"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1145" target="_blank">BOJ 1145 적어도 대부분의 배수</a>

<br>

### 💡 조건

1.  다섯 개의 자연수가 있다. 이 수의 적어도 대부분의 배수는 위의 수 중 적어도 세 개로 나누어 지는 가장 작은 자연수이다.
2.  서로 다른 다섯 개의 자연수가 주어질 때, 적어도 대부분의 배수를 출력하는 문제
3.  100보다 작거나 같은 자연수이고, 서로 다른 수이다.
4.  **브루트포스 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
1 2 3 4 5
```

#### 실행결과

```py
4
```

<br>

### ⌨️ 문제 풀이

1.  math 라이브러리의 lcm 함수를 사용하여 문제를 풀었다.
2.  5개의 숫자 중 3개를 뽑아 최소공배수를 구해 출력하면 된다.
3.  math 라이브러리의 lcm 함수는 python 3.9 버전부터 사용이 가능하다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from math import lcm

arr = list(map(int, stdin.readline().split()))
res = int(1e9)

for i in range(5):
    for j in range(i + 1, 5):
        for k in range(j + 1, 5):
            res = min(res, lcm(arr[i], arr[j], arr[k]))
print(res)
```

<br>

### 💾 느낀점