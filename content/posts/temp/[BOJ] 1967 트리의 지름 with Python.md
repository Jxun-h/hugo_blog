---
author: ["Jxun-h"]
title: "[BOJ] 1967 트리의 지름 with Python"
date: "2021-10-11"
description: ""
summary: ""
tags: ["BFS", "PS", "너비우선탐색", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1967" target="_blank">BOJ 1967 트리의 지름</a>

<br>

## 💡 조건 및 풀이

1.  노드의 개수 `(1 ≤ n ≤ 10,000)`
2.  첫 번째 정수는 간선이 연결하는 두 노드 중 부모 노드의 번호  
    두 번째 정수는 자식 노드  
    세 번째 정수는 간선의 가중치
3.  부모 노드의 번호가 작은 것이 먼저 입력되고,  
    부모 노드의 번호가 같으면 자식 노드의 번호가 작은 것이 먼저 입력된다.
4.  **BFS 유형의 문제**
5.  루트 노드의 번호는 항상 `1`  
    간선의 가중치는 `100`보다 크지 않은 양의 정수
6.  **트리에 존재하는 모든 경로들 중, 가장 긴 경로를 출력하는 문제**이다.

<br>

<br>

## 🔖 예제 및 실행결과

#### 예제

```
12
1 2 3
1 3 2
2 4 5
3 5 11
3 6 9
4 7 1
4 8 7
5 9 15
5 10 4
6 11 6
6 12 10
```

#### 실행결과

```
45
```

<br>

## ⌨️ 문제 풀이

1.  `BFS` 문제 였지만, 트리의 길이를 구하는 문제라고 하기에 당황을 했다.
2.  `BFS` 를 통해 루트 노드인 1 부터 탐색을 시작해서 가중치가 가장 높은 것을  
    반환받아 변수에 담는다.
3.  변수에는 `(node, cost)` 형식으로 있는데, 이 node 번호를 다시 BFS에 넣어 처리한다.
4.  `3번`을 통해서 반환 된 `(node, cost)` 에서 cost가 답이 된다.
5.  다시 설명하자면,  
    `2번`에서 BFS 로 가장 가중치가 많이 쌓이는 노드를 탐색한다. 이를 `A-node` 라고 하고,  
    `3번`에서 `A-node`에서부터 가장 가중치가 많이 쌓이는 곳으로 순회를 하여 `B-node`라고 한다.  
    문제에서 설명하듯, 이 두 노드가 가장 높은 가중치를 가지고 있는 경로 즉, 지름이 된다.

<br>

## 🖥 소스 코드

```python
from sys import stdin
from collections import deque

n = int(stdin.readline())
tree = [[] for _ in range(n + 1)]
for _ in range(n - 1):
    a, b, c = map(int, stdin.readline().split())
    tree[a].append((b, c))
    tree[b].append((a, c))


def bfs(i):
    visited = set()
    q = deque()
    q.append((i, 0))
    visited.add(i)
    res = (0, 0)

    while q:
        now, cost = q.popleft()
        for n, c in tree[now]:
            if n not in visited:
                visited.add(n)
                t = c + cost
                q.append((n, t))

                if res[1] < t:
                    res = (n, t)

    return res


a = bfs(1)
b = bfs(a[0])
print(b[1])
```

## 💾 느낀점

-   BFS를 응용하여 푸는 문제였다. 두번이나 돌릴 생각을 못해서 헤맸다.
-   문제를 해석하고 압축하는 능력을 더 키우고, 생각의 전환을 하는 습관을 길러야겠다.