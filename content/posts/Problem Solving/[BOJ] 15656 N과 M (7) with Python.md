---
author: ["Jxun-h"]
title: "[BOJ] 15656 N과 M (7) with Python"
date: "2023-04-18 17:32:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "백트래킹", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/15656" target="_blank">BOJ 15656 N과 M (7)</a>

<br>

### 💡 조건

1.  N개의 자연수와 자연수 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하는 문제.  
    N개의 자연수는 모두 다른 수이다.
2.  **N개의 자연수 중에서 M개를 고른 수열  
    같은 수를 여러 번 골라도 된다.**
3.  첫째 줄에 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 7)
4.  둘째 줄에 N개의 수가 주어진다. 입력으로 주어지는 수는 10,000보다 작거나 같은 자연수이다.
5.  한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다. 중복되는 수열을 여러 번 출력하면 안되며,  
    수열은 공백으로 구분해서 출력해야 한다. 수열은 사전 순으로 증가하는 순서로 출력해야 한다.
6.  **백트래킹** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
3 1
4 5 2
```

#### 실행결과 1

```py
2
4
5
```

#### 예제 2

```py
4 2
9 8 7 1
```

#### 실행결과 2

```py
1 1
1 7
1 8
1 9
7 1
7 7
7 8
7 9
8 1
8 7
8 8
8 9
9 1
9 7
9 8
9 9
```

#### 예제 3

```py
3 3
1231 1232 1233
```

#### 실행결과 3

```py
1231 1231 1231
1231 1231 1232
1231 1231 1233
1231 1232 1231
1231 1232 1232
1231 1232 1233
1231 1233 1231
1231 1233 1232
1231 1233 1233
1232 1231 1231
1232 1231 1232
1232 1231 1233
1232 1232 1231
1232 1232 1232
1232 1232 1233
1232 1233 1231
1232 1233 1232
1232 1233 1233
1233 1231 1231
1233 1231 1232
1233 1231 1233
1233 1232 1231
1233 1232 1232
1233 1232 1233
1233 1233 1231
1233 1233 1232
1233 1233 1233
```

<br>

### ⌨️ 문제 풀이

1.  순회하는 arr의 원소를 res 배열에 넣으면서 cnt가 m과 같아 질 때, res의 원소를 출력한다.
2.  setrecursionlimit을 반드시 해주어야 한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin, setrecursionlimit

setrecursionlimit(10 ** 7)

n, m = map(int, stdin.readline().split())
arr = list(map(int, stdin.readline().split()))
arr.sort()


def f(res, cnt):
    if cnt == m:
        print(*res)
        return

    for i in arr:
        f(res + [i], cnt + 1)


f([], 0)
```