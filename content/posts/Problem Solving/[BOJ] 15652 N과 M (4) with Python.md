---
author: ["Jxun-h"]
title: "[BOJ] 15652 N과 M (4) with Python"
date: "2023-04-18 16:15:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "백트래킹", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/15652" target="_blank">BOJ 15652 N과 M (4)</a>

<br>

### 💡 조건

1.  자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하시오.
2.  **1부터 N까지 자연수 중에서 M개를 고른 수열  
    같은 수를 여러 번 골라도 된다.  
    고른 수열은 비내림차순이어야 한다.  
    길이가 K인 수열 A가 A1 ≤ A2 ≤ ... ≤ AK-1 ≤ AK를 만족하면, 비내림차순이라고 한다.**
3.  첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)
4.  한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다.  
    중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.  
    수열은 사전 순으로 증가하는 순서로 출력해야 한다.
5.  **백트래킹** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
3 1
```

#### 실행결과 1

```py
1
2
3
```

#### 예제 2

```py
4 2
```

#### 실행결과 2

```py
1 1
1 2
1 3
1 4
2 2
2 3
2 4
3 3
3 4
4 4
```

#### 예제 3

```py
3 3
```

#### 실행결과 3

```py
1 1 1
1 1 2
1 1 3
1 2 2
1 2 3
1 3 3
2 2 2
2 2 3
2 3 3
3 3 3
```

<br>

### ⌨️ 문제 풀이

1.  N과 M (3)의 결과에서 수열이 오름차순인 것만 출력해주면 된다.
2.  수열을 만들 때, res 배열의 마지막 원소가 현재 넣으려는 숫자보다 작거나 같을 때 넣어주는 코드를 넣는다.

<br>

### 🖥 소스 코드

```py
from sys import stdin, setrecursionlimit

setrecursionlimit(10 ** 7)
n, m = map(int, stdin.readline().split())


def f(arr, cnt):
    if cnt == m:
        print(*arr)
        return

    for i in range(1, n + 1):
        if m > 1 and len(arr) > 0:
            if arr[-1] <= i:
                f(arr + [i], cnt + 1)
        else:
            f(arr + [i], cnt + 1)


f([], 0)
```