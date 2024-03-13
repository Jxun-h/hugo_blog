---
author: ["Jxun-h"]
title: "[BOJ] 20444 색종이와 가위 with Python"
date: "2022-05-18"
description: ""
summary: ""
tags: ["자료구조", "PS", "이분탐색", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/20444" target="_blank">BOJ 20444 색종이와 가위</a>

<br>

### 💡 조건

1.  색종이를 자를 때는 다음과 같은 규칙을 따른다.
    1.  색종이는 직사각형이며, 색종이를 자를 때는 한 변에 평행하게 자른다.
    2.  자르기 시작했으면, 경로 상의 모든 색종이를 자를 때까지 멈추지 않는다.
    3.  이미 자른 곳을 또 자를 수 없다.

2.  하나의 색종이를 정확히 n번의 가위질로 k개의 색종이 조각으로 만들 수 있는지 궁금해졌다.
3.  정수 n, k가 주어진다. (1 ≤ n ≤ 231-1, 1 ≤ k ≤ 263-1)
4.  n번의 가위질로 k개의 색종이 조각을 만들 수 있다면 YES, 아니라면 NO를 출력한다.
5.  **이분 탐색** 유형의 문제

<br>

## 🔖 예제 및 실행결과

#### 예제

```py
4 9
```

#### 실행결과

```py
YES
```

<br>

## ⌨️ 문제 풀이

1.  종이를 가로로 a번, 세로로 b번 자른다고 하면, (a + 1) * (b + 1) 개로 잘린다.
2.  이 문제에서는 총 n번 자르길 원하고, 가로와 세로를 각각 몇 번 자르는지에 따라 개수는 달라진다.
3.  n = a + b 이다.  
    b = n - a 라고 할 수 있다.
4.  (a + 1) * (b + 1) 식에 b를 대입하면, (a + 1) * (n - a + 1) 개로 바뀐다.
5.  n은 범위가 (2 ** 31 - 1) 까지이기에 하나하나 찾아볼 순 없고, 이분탐색을 사용해야한다.
6.  또한 0 에서 n // 2 까지만 탐색을 해주면 된다.

<br>

### 🖥 소스 코드

```py
import sys

input = sys.stdin.readline
n, k = map(int, input().split())


def f(x):
    return (x + 1) * (n - x + 1)


lo, hi = 0, n // 2 + 1
while lo != hi:

    mid = (lo + hi) // 2
    data = f(mid)

    if data == k:
        print("YES")
        sys.exit(0)

    if data > k:
        hi = mid

    else:
        lo = mid + 1

print("NO")
```
