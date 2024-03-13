---
author: ["Jxun-h"]
title: "[BOJ] 10451 순열 사이클 with Python"
date: "2022-06-14"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/10451" target="_blank">BOJ 10451 순열 사이클</a>

<br>

### 💡 조건

1.  1부터 N까지 정수 N개로 이루어진 순열을 나타내는 방법은 여러 가지가 있다.

2.  순열 그래프 (3, 2, 7, 8, 1, 4, 5, 6) 에는 총 3개의 사이클이 있다. 이러한 사이클을 "순열 사이클" 이라고 한다.

3.  N개의 정수로 이루어진 순열이 주어졌을 때, 순열 사이클의 개수를 구하는 프로그램을 작성하시오.

4.  첫째 줄에 테스트 케이스의 개수 T가 주어진다.  
    각 테스트 케이스의 첫째 줄에는 순열의 크기 N (2 ≤ N ≤ 1,000)이 주어진다. 둘째 줄에는 순열이 주어지며, 각 정수는 공백으로 구분되어 있다.

5.  각 테스트 케이스마다, 입력으로 주어진 순열에 존재하는 순열 사이클의 개수를 출력한다.

6.  **BFS, 그래프탐색** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
2
8
3 2 7 8 1 4 5 6
10
2 1 3 4 5 6 7 9 10 8
```

#### 실행결과

```py
3
7
```

<br>

### ⌨️ 문제 풀이

1.  테스트 케이스 수만큼 입력된 데이터를 문제에 제시된 방법철머 그래프로 만들어서 사이클을 세어주는 문제이다.

2.  그래프를 순회하면서 visited 변수를 set()으로 만들어 주고 방문처리를 해준다.

3.  사이클을 세어준 뒤, 개수를 출력해주면 된다.

<br>

### 🖥 소스 코드

```py
from collections import deque
from sys import stdin, setrecursionlimit

setrecursionlimit(10 ** 6)


def get_cnt(x, graph, visited):
    q = deque()
    q.append(x)
    visited.add(x)

    while q:
        now = q.popleft()

        for y in list(graph[now]):
            if y not in visited:
                q.append(y)
                visited.add(y)

    return 1


def solve(temp):
    global ans
    res = 0
    graph = [[] for _ in range(n + 1)]
    for i in range(n):
        graph[temp[i]].append(arr[i])

    visited = set()
    for i in range(1, n + 1):
        if i not in visited:
            res += get_cnt(i, graph, visited)

    ans = max(res, ans)


for _ in range(int(stdin.readline())):
    n = int(stdin.readline())
    arr = list(map(int, stdin.readline().split()))
    ans = 0

    solve([x for x in range(1, n + 1)])
    print(ans)
```
