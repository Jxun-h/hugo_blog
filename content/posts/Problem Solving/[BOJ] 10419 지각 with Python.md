---
author: ["Jxun-h"]
title: "[BOJ] 10419 지각 with Python"
date: "2023-04-03 16:14:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/10419" target="_blank">BOJ 10419 지각</a>

<br>

### 💡 조건

1.  교수님의 지각시간 0이상의 정수 t와 수업을 일찍 마쳐주는 시간 s 사이에는 s = t**2 의 관계가 있다.
2.  창영이가 궁금한 경우의 수 T(1 ≤ T ≤ 100)가 첫 번째 줄에 주어지고,
3.  이어서 T 개의 줄에 수업시간 d(1 ≤ d ≤ 10,000, d는 정수)가 차례대로 주어진다.
4.  수업시간에 따른 교수님이 지각할 수 있는 최대 시간 t를 정수로 구해서 출력한다.
5.  지각할 수 있는 최대의 시간을 알아보는 문제
6.  **브루트포스** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
5
1
2
5
6
7
```

#### 실행결과 1

```py
0
1
1
2
2
```

<br>

### ⌨️ 문제 풀이

1.  지각할 수 있는 최대시간을 구하려면, 수업시간 d의 최대값이 얼마인지 확인해봐야한다.
2.  지각할 수 있는 최대시간은 100부터 -1씩 줄여나가 i * 1 ** 2의 값이 d보다 같거나 작아질 때를 찾으면 된다.
3.  만약 d = 1 이라면 0이 출력되어야 하기 때문에 ans의 값은 0으로 초기화를 한 뒤 계산한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

for _ in range(int(stdin.readline())):
    d = int(stdin.readline())
    ans = 0
    for i in range(100, 0, -1):
        if i + i ** 2 <= d:
            ans = i
            break
    print(ans)
```