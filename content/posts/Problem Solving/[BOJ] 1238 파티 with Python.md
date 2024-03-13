---
author: ["Jxun-h"]
title: "[BOJ] 1238 파티 with Python"
date: "2022-06-07"
description: ""
summary: ""
tags: ["자료구조", "PS", "다익스트라", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1238" target="_blank">BOJ 1238 파티</a>

<br>

### 💡 조건

1.  N개의 숫자로 구분된 각각의 마을에 한 명의 학생이 살고 있다.

2.  N명의 학생이 X (1 ≤ X ≤ N)번 마을에 모여서 파티를 벌이기로 했다.  
    이 마을 사이에는 총 M개의 단방향 도로들이 있고 i번째 길을 지나는데 Ti(1 ≤ Ti ≤ 100)의 시간을 소비한다.

3.  각각의 학생들은 파티에 참석하기 위해 걸어가서 다시 그들의 마을로 돌아와야 한다.  
    하지만 이 학생들은 워낙 게을러서 최단 시간에 오고 가기를 원한다.

4.  이 도로들은 단방향이기 때문에 아마 그들이 오고 가는 길이 다를지도 모른다.  
    N명의 학생들 중 오고 가는데 가장 많은 시간을 소비하는 학생은 누구일지 구하여라.

5.  N(1 ≤ N ≤ 1,000), M(1 ≤ M ≤ 10,000), X가 공백으로 구분되어 입력된다.  
    시작점과 끝점이 같은 도로는 없으며, 시작점과 한 도시 A에서 다른 도시 B로 가는 도로의 개수는 최대 1개이다.  
    모든 학생들은 집에서 X에 갈수 있고, X에서 집으로 돌아올 수 있는 데이터만 입력으로 주어진다.

6.  **그래프탐색, 다익스트라** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4 8 2
1 2 4
1 3 2
1 4 7
2 1 1
2 3 5
3 1 2
3 4 4
4 2 3
```

#### 실행결과

```py
10
```

<br>

### ⌨️ 문제 풀이

1.  **"최단 시간에 오고 가기를 원한다."** 라는 대목에서 다익스트라를 생각해볼 수 있다.  
    또한 문제에서 M개의 단방향 도로들이 있다는 정보가 있다.

2.  (1)번의 정보를 통해 단방향 그래프에서 최단거리를 찾으면 된다는 결론이 나온다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
import heapq

n, m, x = map(int, stdin.readline().split())
graph = [[] for _ in range(n + 1)]
ans = [0 for _ in range(n)]

for _ in range(m):
    a, b, c = map(int, stdin.readline().split())
    graph[a].append((c, b))


def solve(start):
    q = []
    heapq.heappush(q, (0, start))
    dist = [int(1e9) for _ in range(n + 1)]
    dist[start] = 0

    while q:
        cost, now = heapq.heappop(q)

        for d, next_pos in graph[now]:
            if dist[next_pos] > cost + d:
                dist[next_pos] = cost + d
                heapq.heappush(q, (cost + d, next_pos))

    return dist


r = -1
for i in range(1, n + 1):
    if i != x:
        go = solve(i)[x]
        goal = solve(x)[i]
        r = max(r, go + goal)

print(r)
```
