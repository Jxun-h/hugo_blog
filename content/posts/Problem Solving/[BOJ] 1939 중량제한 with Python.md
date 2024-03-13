---
author: ["Jxun-h"]
title: "[BOJ] 1939 중량제한 with Python"
date: "2022-07-12 15:12:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "이분탐색", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1939" target="_blank">BOJ 1939 중량제한</a>

<br>

### 💡 조건

1.  N(2 ≤ N ≤ 10,000)개의 섬으로 이루어진 나라가 있다. 이들 중 몇 개의 섬 사이에는 다리가 설치되어 있어서 차들이 다닐 수 있다.

2.  영식 중공업에서는 두 개의 섬에 공장을 세워 두고 물품을 생산하는 일을 하고 있다.  
    물품을 생산하다 보면 공장에서 다른 공장으로 생산 중이던 물품을 수송해야 할 일이 생기곤 한다.  
    그런데 각각의 다리마다 중량제한이 있기 때문에 무턱대고 물품을 옮길 순 없다.  
    만약 **중량제한을 초과하는 양의 물품이 다리를 지나게 되면 다리가 무너지게 된다.**

3.  첫째 줄에 N, M(1 ≤ M ≤ 100,000)이 주어진다.  
    다음 M개의 줄에는 다리에 대한 정보를 나타내는 세 정수 A, B(1 ≤ A, B ≤ N), C(1 ≤ C ≤ 1,000,000,000)가 주어진다.

4.  이는 A번 섬과 B번 섬 사이에 중량제한이 C인 다리가 존재한다는 의미이다.  
    서로 같은 두 섬 사이에 여러 개의 다리가 있을 수도 있으며, **모든 다리는 양방향이다.**

5.  마지막 줄에는 공장이 위치해 있는 섬의 번호를 나타내는 서로 다른 두 정수가 주어진다.  
    공장이 있는 두 섬을 연결하는 경로는 항상 존재하는 데이터만 입력으로 주어진다.

6.  **BFS, 이분탐색** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3 3
1 2 2
3 1 3
2 3 2
1 3
```

#### 실행결과

```py
3
```

<br>

### ⌨️ 문제 풀이

1.  지문을 통해 파악할 수 있는 것은 모든 섬을 연결하는 다리가 양방향이라는 것이다.  
    양방향 그래프를 만들기 위해 graph 리스트를 생성하고, 섬과 섬 번호, 간선의 비용인 (a,b,c) 를 입력받아 양방향 그래프를 만들어준다.

2.  출발지점과 도착지점을 입력받아 start, end에 저장한 후 그래프 순회를 위한 BFS함수를 구현한다.  
    이 때, 들고 갈 수 있는 최대 중량 값 mid 를 기준으로 조건문을 작성하여 방문처리 및 큐에 노드 번호를 추가해야한다.  
    조건은 두가지다. 방문하지 않은 노드, mid 보다 cost가 크거나 같을 때 이다.

3.  최대 중량값을 1부터 1,000,000,000 까지 차례대로 순회를 돌면 시간초과가 나오기 때문에 여기서 이분탐색을 통해서 mid 값을 정해주어야한다.

4.  BFS에서 True 를 반환했다면, ans가 mid 보다 작을 경우 갱신한다.


<br>

### 🖥 소스 코드

```py
from sys import stdin
from collections import deque

n, m = map(int, stdin.readline().split())
graph = [[] for _ in range(n + 1)]

for _ in range(m):
    a, b, c = map(int, stdin.readline().split())
    graph[a].append((b, c))
    graph[b].append((a, c))

start, end = map(int, stdin.readline().split())
l, r = 0, int(1e9)


def solve(mid):
    q = deque()
    q.append(start)
    visited[start] = True

    while q:
        now = q.popleft()
        if now == end:
            return True

        for node, cost in graph[now]:
            if not visited[node] and mid <= cost:
                q.append(node)
                visited[node] = True

    return False


ans = 0
while l <= r:
    mid = (l + r) // 2
    visited = [False for _ in range(n + 1)]

    if solve(mid):
        ans = max(ans, mid)
        l = mid + 1

    else:
        r = mid - 1

print(ans)
```
