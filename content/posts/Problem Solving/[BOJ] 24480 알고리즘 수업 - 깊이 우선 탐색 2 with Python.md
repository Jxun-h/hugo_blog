---
author: ["Jxun-h"]
title: "[BOJ] 24480 알고리즘 수업 - 깊이 우선 탐색 2 with Python"
date: "2023-04-10 17:23:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "정렬", "DFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/24480" target="_blank">BOJ 24480 알고리즘 수업 - 깊이 우선 탐색 2</a>

<br>

### 💡 조건

1.  N개의 정점과 M개의 간선으로 구성된 **무방향 그래프(undirected graph)**가 주어진다.
2.  정점 번호는 1번부터 N번이고 모든 간선의 가중치는 1이다.
3.  정점 R에서 시작하여 깊이 우선 탐색으로 노드를 방문할 경우 노드의 방문 순서를 출력하자.
4.  깊이 우선 탐색 의사 코드는 다음과 같다. 인접 정점은 **내림차순**으로 방문한다.
5.  첫째 줄에 정점의 수 N (5 ≤ N ≤ 100,000), 간선의 수 M (1 ≤ M ≤ 200,000), 시작 정점 R (1 ≤ R ≤ N)이 주어진다.
6.  다음 M개 줄에 간선 정보 u v가 주어지며 정점 u와 정점 v의 가중치 1인 양방향 간선을 나타낸다.  
    (1 ≤ u < v ≤ N, u ≠ v) 모든 간선의 (u, v) 쌍의 값은 서로 다르다.
7.  첫째 줄부터 N개의 줄에 정수를 한 개씩 출력한다. **i번째 줄에는 정점 i의 방문 순서를 출력한다.**  
    시작 정점의 방문 순서는 1이다. 시작 정점에서 방문할 수 없는 경우 0을 출력한다.
8.  **DFS, 정렬** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
5 5 1
1 4
1 2
2 3
2 4
3 4
```

#### 실행결과 1

```py
1
4
3
2
0
```

<br>

### ⌨️ 문제 풀이

1.  문제의 지문을 먼저 잘 살펴보자.  
    **무방향 그래프(undirected graph)**, 인접 정점은 **내림차순**으로 방문,
2.  무방향 그래프는 양방향 그래프이기 때문에 간선 정보를 그래프에 저장할 때 a에서 b, b에서 a를 저장해줘야 한다.
3.  인접 정점은 내림차순으로 방문한다고 했기 때문에, 방문이 가능한 다음 노드는 내림차순 정렬을 해주어야 한다.
4.  (3), (4)번을 유의해야하며, 파이썬의 경우 setrecursionlimit을 하는게 안전하다.
5.  방문을 하면서 방문한 순서를 visited(방문처리배열)에 적어 출력해주면 된다.

<br>

### 🖥 소스 코드

```py
from sys import stdin, setrecursionlimit

setrecursionlimit(10 ** 7)

n, m, r = map(int, stdin.readline().split())
graph = [[] for _ in range(n + 1)]
visited = [0 for _ in range(n + 1)]
cnt = 1

for _ in range(m):
    a, b = map(int, stdin.readline().split())
    graph[a].append(b)
    graph[b].append(a)


def dfs(r):
    global cnt
    visited[r] = cnt
    graph[r].sort(reverse=True)
    for node in graph[r]:
        if visited[node] == 0:
            cnt += 1
            dfs(node)


dfs(r)
for i in visited[1:]:
    print(i)
```