---
author: ["Jxun-h"]
title: "[BOJ] 6118 숨바꼭질 with Python"
date: "2021-12-01"
description: ""
summary: ""
tags: ["자료구조", "PS", "너비우선탐색", "BFS", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/6118" target="_blank">BOJ 6118 숨바꼭질</a>

<br>

### 💡 조건

1.  헛간의 개수 `(2 <= N <= 20,000)`, 1부터 세아린다.
2.  모든 헛간은 `(1<= M <= 50,000)`개의 **양방향 길**로 이어져 있다.
3.  냄새는 1번 헛간에서의 거리가 멀어질수록 감소한다.  
    `거리 = 지나야 하는 길의 최소 개수.`
4.  `숨어야 하는 가장 거리가 먼 헛간 번호`, `가장 거리가 먼 헛간까지의 거리`, `가장 거리가 먼 헛간과 같은 거리를 가지는 헛간의 수`  
    를 차례대로 출력하며, 가장 거리가 먼 헛간 번호가 여러개라면 가장 작은 수를 출력한다.
5.  **너비 우선 탐색(BFS)**유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
6 7
3 6
4 3
3 2
1 3
1 2
2 4
5 2
```

#### 실행결과

```python
4 2 3
```

<br>

### ⌨️ 문제 풀이

1.  양방향으로 움직일 수 있는 노드들을 연결하기 위해 2차원 리스트인 `arr`을 생성한 후 데이터를 입력한다.
2.  결과 값을 저장하고, 헛간의 번호를 의미하는 `res` 2차원 리스트를 생성한다.  
    가장 먼 헛간의 거리를 저장할 `max_dist` 변수도 생성한다.
3.  너비 우선 탐색 알고리즘을 호출하는데, 큐에는 `(거리, 노드번호)`를 넣어준다.  
    큐가 빌 때까지 반복하면서, 해당 헛간과 연결되어 있는 헛간을 순차적으로 방문한다.  
    큐에서 데이터를 `pop()` 하여 나온 거리 데이터가 현재 `max_dist` 보다 크다면 갱신한다.
4.  방문한 헛간은 이미 방문했던 헛간이라는 정보를 저장하기 위해 `visited` 집합 자료형에 노드번호를 저장한다.
5.  헛간의 거리는 모두 1씩이기에, 큐에 `(현재 헛간과의 거리 + 1, 노드번호)` 를 저장한다.
6.  `res` 리스트에 거리 + 1에 해당하는 리스트에 노드 번호를 저장한다.  
    `res` 리스트에는 가장 먼 거리에 해당하는 원소 리스트에 같은 거리를 가진 헛간의 번호들이 저장된다.
7.  문제에서 요구한 것들을 출력한다.  
    숨어야 하는 헛간의 번호 = `min(res[max_dist])`  
    숨어야 하는 헛간까지의 거리 = `max_dist`  
    숨어야 하는 헛간까지의 거리와 같은 거리를 가진 헛간들 = `len(res[max_dist])`

<br>

### 🖥 소스 코드

```python
from sys import stdin
from collections import deque

n, m = map(int, stdin.readline().split())
arr = [[] for _ in range(n + 1)]
for _ in range(m):
    a, b = map(int, stdin.readline().split())
    arr[a].append(b)
    arr[b].append(a)

res = [[] for _ in range(20001)]
max_dist = -1e9


def bfs(n):
    global max_dist
    q = deque()
    q.append((0, n))
    visited = set()
    visited.add(n)

    while q:
        dist, now = q.popleft()
        max_dist = max(max_dist, dist)
        for node in arr[now]:
            if node not in visited:
                visited.add(node)
                q.append((dist + 1, node))
                res[dist + 1].append(node)


bfs(1)
print(min(res[max_dist]), max_dist, len(res[max_dist]))
```

<br>

### 💾 느낀점

1.  BFS 응용 문제이기 때문에 풀이를 하는데에는 오래 걸리지 않았다.
2.  그래프 이론 및 BFS 문제는 조금씩 더 풀어서 내것으로 만들어도 더 좋을 것 같다.