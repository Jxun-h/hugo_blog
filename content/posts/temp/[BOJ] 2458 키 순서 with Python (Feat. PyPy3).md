---
author: ["Jxun-h"]
title: "[BOJ] 2458 키 순서 with Python (Feat. PyPy3)"
date: "2021-09-02"
description: ""
summary: ""
tags: ["플로이드-와샬", "PS", "그래프이론", "알고리즘", "프로그래머스"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2458" target="_blank">BOJ 2458 키 순서</a>

<br>

## 💡 조건 및 풀이

1.  `1번부터 N번까지` 번호가 붙여져 있는 학생들끼리 두 명씩 키를 비교했다.
2.  `N`명의 학생들은 모두 키가 다르다.
3.  **플로이드와샬 알고리즘**으로 해결이 가능한 문제이다.
4.  `2 <= N <= 500`, `0 <= M <= N(N-1)/2`
5.  `M`개의 줄에 두 학생의 키를 비교한 결과를 나타내는 두 양의 정수 `a, b`가 주어진다.
6.  `a, b == a가 b보다 작다`
7.  **자신의 키가 몇번째인지 알 수 있는 학생의 수를 구하는 문제**

<br>

## 🖥 소스 코드

```python
from sys import stdin

n, m = map(int, stdin.readline().split())
inf = int(1e9)
graph = [[inf] * (n + 1) for _ in range(n + 1)]

for _ in range(m):
    a, b = map(int, stdin.readline().split())
    graph[b][a] = 1

for i in range(1, n + 1):
    for j in range(1, n + 1):
        for k in range(1, n + 1):
            if j == k:
                graph[j][k] = 0
                continue
            if graph[j][k] > graph[j][i] + graph[i][k]:
                graph[j][k] = graph[j][i] + graph[i][k]


res = n
for i in range(1, n + 1):
    checker = 1
    for j in range(1, n + 1):
        if graph[i][j] == inf and graph[j][i] == inf:
            res -= 1
            checker = 0
        if not checker:
            break

print(res)
```

<br>

## 🔖 예제 및 실행결과

#### 예제

```python
6 7
1 3
1 5
3 4
5 4
4 2
4 6
5 2
```

#### 실행결과

```python
2
```

<br>

## ⌨️ 문제 풀이

1.  최소 거리를 정해준다고 생각하고 `플로이드 와샬`을 사용하기 위해 2차원 리스트를 만들고  
    `INF` 값을 넣어 리스트를 초기화했다.
2.  `a, b` 값을 입력받게 되면 `a 가 b 보다 작다` 라는 조건에 따라, 2차원 리스트에 `graph[b].append(a)`
3.  `플로이드 와샬` 알고리즘 실행
4.  자신의 키가 몇등인지 알 수있는 사람을 처음부터 `N`명이라고 정의한 뒤 1번 학생부터 순차적으로  
    2중 반복문을 사용해 플로이드 와샬로 만든 2차원 리스트에 접근
5.  `if graph[i][j] == inf and graph[j][i] == inf:`  
    **i번 학생이 j번 학생과의 작다, 크다의 정보가 아무것도 없다면** `res -= 1`
6.  2중 반복문을 빠져나오기 위한 checker변수에 0을 넣어주고(False) 반복문 탈출
7.  `PyPy3` 제출

<br>

## 🖥 소스 코드

```python
from sys import stdin

n, m = map(int, stdin.readline().split())
inf = int(1e9)
graph = [[inf] * (n + 1) for _ in range(n + 1)]

for _ in range(m):
    a, b = map(int, stdin.readline().split())
    graph[b][a] = 1

for i in range(1, n + 1):
    for j in range(1, n + 1):
        for k in range(1, n + 1):
            if j == k:
                graph[j][k] = 0
                continue
            if graph[j][k] > graph[j][i] + graph[i][k]:
                graph[j][k] = graph[j][i] + graph[i][k]


res = n
for i in range(1, n + 1):
    checker = 1
    for j in range(1, n + 1):
        if graph[i][j] == inf and graph[j][i] == inf:
            res -= 1
            checker = 0
        if not checker:
            break

print(res)
```

<br>

## 💾 느낀점

-   문제를 보자마자 `플로이드와샬 알고리즘`과 `유니온-파인드`가 생각났다.  
    `유니온-파인드`로 구현을 하려다보니 절대 아닌 것 같아 `플로이드와샬`을 사용하기로 했다.
-   아는 분들의 이야기를 들어보니 `BFS`로 구현하셨다고 했다.
-   플로이드 와샬 알고리즘으로 해결했을 때, `Python3` 로 시간초과가 생겼으며, `PyPy3` 는 통과
-   `BFS`로 풀이하는 방법도 구현해봐야겠다.
-   문제를 풀시간은 없는데 생각할 시간이 너무 길다. 아직 숙달이 되지 못한 것이라고 생각하고 더 풀어봐야겠다.