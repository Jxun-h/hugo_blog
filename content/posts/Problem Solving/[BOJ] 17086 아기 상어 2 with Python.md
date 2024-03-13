---
author: ["Jxun-h"]
title: "[BOJ] 17086 아기 상어 2 with Python"
date: "2022-07-17 22:03:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "우선순위 큐", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/17086" target="_blank">BOJ 17086 아기 상어 2</a>

<br>

### 💡 조건

1.  N×M 크기의 공간에 아기 상어 여러 마리가 있다. 공간은 1×1 크기의 정사각형 칸으로 나누어져 있다. 한 칸에는 아기 상어가 최대 1마리 존재한다.  
    N과 M(2 ≤ N, M ≤ 50)

2.  어떤 칸의 안전 거리는 그 칸과 가장 거리가 가까운 아기 상어와의 거리이다.  
    두 칸의 거리는 하나의 칸에서 다른 칸으로 가기 위해서 지나야 하는 칸의 수이고, 이동은 인접한 8방향(대각선 포함)이 가능하다.

3.  0은 빈 칸, 1은 아기 상어가 있는 칸이다.

4.  빈 칸과 상어의 수가 각각 한 개 이상인 입력만 주어진다.

5.  안전 거리가 가장 큰 칸을 구하는 문제.

6.  **heapq, 우선순위 큐** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
5 4
0 0 1 0
0 0 0 0
1 0 0 0
0 0 0 0
0 0 0 1
```

#### 실행결과 1

```py
2
```

#### 예제 2

```py
7 4
0 0 0 1
0 1 0 0
0 0 0 0
0 0 0 1
0 0 0 0
0 1 0 0
0 0 0 1
```

#### 실행결과 2

```py
2
```

<br>

### ⌨️ 문제 풀이

1.  문제에서 보면, N과 M이 각각 최대 50이기 때문에 최대 50 * 50 짜리 2차원 배열을 사용할 수 있다.

2.  1은 아기 상어이며, 0은 안전한 칸이다. 이 문제의 핵심은 우선순위 큐를 사용하는 것인데, 우선순위 큐란 무엇인가?  
    우선순위 큐는 먼저 들어오는 데이터가 아니라, 우선순위가 높은 데이터가 먼저 나가는 형태의 자료구조이다.

3.  안전거리의 값을 우선순위로 두어 큐에 저장하면서 8 방향으로, 방문하지 않은 칸을 큐에 넣어준다.  
    파이썬의 heapq 에서는 최소 힙(Min Heap)의 형태로 데이터를 저장한다.  
    최소 힙의 루드 노드는 모든 노드보다 작은 값을 가지고 있다.

4.  ans 의 값을 -1로 초기화하고, board를 한칸씩 순회하면서 0인 경우에 solve() 함수에 좌표값을 넘겨준다.  
    solve() 함수에서는 heapq 를 사용해 BFS를 수행하면서, 8 방향을 탐색한다.  
    안전거리는 **어떤 칸의 안전 거리는 그 칸과 가장 거리가 가까운 아기 상어와의 거리** 이다.

5.  (4)번처럼 탐색을 하면 가장 가까운 아기 상어의 칸을 탐색할 수 있으며, 힙 큐에서 뽑은 좌표의 값이 아기 상어일 경우, dist를 반환한다.

6.  반환된 dist를 ans와 비교해 더 큰 값으로 갱신한 후, board 를 모두 순회했다면 ans를 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
import heapq

n, m = map(int, stdin.readline().split())
arr, shark = [], []
dx, dy = [1, 0, 0, -1, 1, -1, 1, -1], [0, 1, -1, 0, 1, -1, -1, 1]
ans = -1

for i in range(n):
    data = list(map(int, stdin.readline().split()))
    arr.append(data)
    for j in range(m):
        if data[j] == 1:
            shark.append((i, j))


def solve(x, y):
    q = []
    heapq.heappush(q, (0, x, y))
    visited = set()
    visited.add((x, y))

    while q:
        dist, x, y = heapq.heappop(q)
        if arr[x][y] == 1:
            return dist

        for i in range(8):
            nx, ny = dx[i] + x, dy[i] + y
            if 0 <= nx < n and 0 <= ny < m:
                if (nx, ny) not in visited:
                    heapq.heappush(q, (dist + 1, nx, ny))
                    visited.add((nx, ny))


for i in range(n):
    for j in range(m):
        if arr[i][j] == 0:
            res = solve(i, j)
            if res > ans:
                ans = res

print(ans)
```

<br>

### 💾 느낀점

1.  BFS 알고리즘을 Heapq를 사용해 8방향으로 탐색하고 결과를 도출하는 것에 대해 좋은 경험을 쌓을 수 있는 문제였던 것 같다.