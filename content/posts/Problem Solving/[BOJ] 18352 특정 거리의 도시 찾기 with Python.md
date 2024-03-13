---
author: ["Jxun-h"]
title: "[BOJ] 18352 특정 거리의 도시 찾기 with Python"
date: "2021-08-30"
description: ""
summary: ""
tags: ["BFS", "PS", "너비우선탐색", "알고리즘", "백준", "BOJ", "다익스트라"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/18352" target="_blank">BOJ 18352 특정 거리의 도시 찾기</a>

<br>

### 💡 조건 및 풀이

1.  `1번부터 N번까지의 도시`와 `M개의 단방향 도로`가 존재. 모든 도로의 거리는 1.
2.  특정한 도시 `X`로부터 출발하여 도달할 수 있는 모든 도시 중에서, `최단 거리`가 정확히 `K`인 모든 도시들의 번호를 출력.
3.  **BFS 유형의 문제**
4.  도달할 수 있는 도시 중에서, 최단 거리가 K인 도시가 하나도 존재하지 않으면 -1을 출력

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
4 4 2 1
1 2
1 3
2 3
2 4
```

#### 실행결과

```python
4
```

<br>

### ⌨️ 문제 풀이

1.  모든 도시가 1부터 시작하기 때문에 `graph` 리스트의 길이를 `n + 1`로 한다.
2.  단방향 간선이기 때문에 `graph[a].append(b)`
3.  `bfs(x)`에서 사용하는 방문처리용 자료구조를 `list`가 아닌 `set`으로 사용했다.
4.  `queue`에는 현재 노드와 비용에 대해서 튜플로 만들어 넣어준다.  
    단, 이미 방문했던 노드는 다시 방문하지 않는다. = `visited`

<br>

### 🖥 소스 코드

```python
from sys import stdin
from collections import deque

n, m, k, x = map(int, stdin.readline().split())
graph = [[] for _ in range(n + 1)]

for i in range(m):
    a, b = map(int, stdin.readline().split())
    graph[a].append(b)

def bfs(x):
    res = []
    visited = set()
    q = deque()
    q.append((x, 0))
    visited.add(x)

    while q:
        now, cost = q.popleft()

        if cost == k:
            res.append(now)

        for i in graph[now]:
            if i not in visited:
                q.append((i, cost + 1))
                visited.add(i)

    if not res:
        print(-1)
    else:
        res.sort()
        for i in res:
            print(i)

bfs(x)
```

<br>

### 💾 느낀점

-   다익스트라, BFS 문제의 유형은 더 많이 풀어봐야겠다.
-   개념이 조금 익혀져 있는 다익스트라 기본 문제를 풀어서 쉽게 풀 수 있었다.
-   플로이드 와샬로는 시도해보지 않았다.