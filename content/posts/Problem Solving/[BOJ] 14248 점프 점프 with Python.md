---
author: ["Jxun-h"]
title: "[BOJ] 14248 점프 점프 with Python"
date: "2022-02-10"
description: ""
summary: ""
tags: ["자료구조", "PS", "탐색", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/14248" target="_blank">BOJ 14248 점프 점프</a>

<br>

### 💡 조건

1.  돌다리의 돌 개수 n이 주어진다.(1≤n≤100,000)
2.  그 위치에서 점프할 수 있는 거리 Ai (1≤Ai≤100,000)
3.  현재위치에서 다른 돌을 적절히 밟아 해당하는 위치로 이동이 가능하다고 할 때, 영우가 방문 가능한 돌들의 개수를 구하는 문제.
4.  **탐색 알고리즘**유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5
1 4 2 2 1
3
```

#### 실행결과

```py
5
```

<br>

### ⌨️ 문제 풀이

1.  입력으로 받은 점프할 수 있는 거리를 그래프에 넣어준다.  
    인덱스 에러를 방지하기 위해 arr 리스트의 크기는 n + 1로 해준다.
2.  (1) 번 작업에서, 현재 위치에서 이동할 수 있는 거리를 빼거나 더했을 때, 리스트 인덱스의 범위인지 확인하고 넣는다.
3.  BFS 알고리즘을 이용하여 방문처리 배열을 만들고 방문해준다.
4.  정답은 영우가 방문 할 수 있는 돌들의 개수이니, visited 리스트의 길이 + 1을 출력한다.
5.  영우가 처음 밟은 돌도 포함이니까 + 1 해준다.  
    시작하는 돌을 visited에 먼저 넣어주고 시작했다면 + 1을 굳이 하지 않아도 된다.

<br>

## 🖥 소스 코드

```py
from sys import stdin
from collections import deque

n = int(stdin.readline())
arr = [0] + list(map(int, stdin.readline().split()))
graph = [[] for _ in range(n + 1)]
s = int(stdin.readline())
for i in range(1, n + 1):
    if 0 < i + arr[i] < n + 1:
        graph[i].append(i + arr[i])

    if 0 < i - arr[i] < n + 1:
        graph[i].append(i - arr[i])



def solve(s):
    q = deque()
    q.append(s)
    visited = set()

    while q:
        now = q.popleft()
        for x in graph[now]:
            if x not in visited:
                visited.add(x)
                q.append(x)

    return len(visited)

print(solve(s) + 1)
```

<br>

### 💾 느낀점

1.  재미있는 BFS 문제였습니다.
2.  개굴 개굴