---
author: ["Jxun-h"]
title: "[BOJ] 18243 Small World Network with Python"
date: "2022-03-01"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "그래프 이론", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/18243" target="_blank">BOJ 18243 Small World Network</a>

<br>

### 💡 조건

1.  첫 번째 줄에 지구에 있는 사람의 수 N과 친구 관계의 개수 K.  
    (1 ≤ N ≤ 100, 0 ≤ K ≤ N×(N-1)/2)
2.  모든 사람은 1부터 N까지 번호가 매겨져 있다.
3.  두 번째 줄부터 K+1번째 줄까지 친구 관계를 나타내는 A B가 한 줄에 하나씩 주어진다.  
    (1 ≤ A, B ≤ N)
4.  A와 B가 친구면 B와 A도 친구다. 자기 자신과 친구인 경우는 없다.  
    A와 B의 친구 관계는 중복되어 입력되지 않는다.
5.  해당 네트워크가 작은 세상 네트워크를 만족하면  
    "Small World!"를, 만족하지 않는다면 "Big World!"를 출력
6.  **BFS, 그래프 이론** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
10 8
1 2
2 3
3 4
4 5
6 7
7 8
8 9
9 10
```

#### 실행결과

```py
Big World!
```

<br>

### ⌨️ 문제 풀이

1.  네트워크 상의 친구 사이는 양방향 간선이라고 볼 수 있다.
2.  그래프로 사용할 network 라는 리스트를 만들고, 그래프에 입력한다.
3.  1번 노드부터 bfs() 알고리즘을 수행하면서 q 에 (노드번호, dist)를 넣어 수행한다.  
    dist = 0 부터 시작한다.
4.  bfs가 수행되면서 dist가 6을 초과하면, False를 반환한다.
5.  visited (방문 처리 set)의 길이가 만약 노드 총 개수 n과 같지 않다면 False 를 반환.
6.  반환받은 bfs 의 결과값이 False라면 "Big World!"  
    반환받은 bfs 의 결과값이 True라면 "Small World!"

<br>

### 🖥 소스 코드

```py
from sys import stdin
from collections import deque


n, k = map(int, stdin.readline().split())
network = [[] for _ in range((n + 1))]
tf = True

for i in range(k):
    a, b = map(int, stdin.readline().split())
    network[a].append(b)
    network[b].append(a)


def bfs(root):
    visited = set()
    visited.add(root)
    q = deque()
    q.append((root, 0))

    while q:
        now, dist = q.popleft()
        if dist > 6:
            return False

        for node in network[now]:
            if node not in visited:
                visited.add(node)
                q.append((node, dist + 1))

    if len(visited) == n:
        return True
    else:
        return False


for i in range(1, n + 1):
    if not bfs(i):
        tf = False
        break

if tf:
    print("Small World!")
else:
    print("Big World!")
```

<br>

### 💾 느낀점

1.  BFS로는 풀이를 가능했지만, 플로이드-와샬 알고리즘에서는 실패했었다.
2.  (1)번 의 이유는 dist > 6 의 조건을 처리하지 못해서였다.