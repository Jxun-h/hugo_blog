---
author: ["Jxun-h"]
title: "[BOJ] 1743 음식물 피하기 with Python"
date: "2021-10-18"
description: ""
summary: ""
tags: ["구현", "PS", "시뮬레이션", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1743" target="_blank">BOJ 1743 음식물 피하기</a>

<br>

### 💡 조건

1.  통로의 세로 길이 `N(1 ≤ N ≤ 100)`  
    통로의 가로 길이 `M(1 ≤ M ≤ 100)`  
    음식물 쓰레기의 개수 `K(1 ≤ K ≤ N×M)`  
    `K`개의 줄에 음식물이 떨어진 좌표 `(r, c)`
2.  **DFS 유형의 문제(깊이우선탐색)**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
3 4 5
3 2
2 2
3 1
2 3
1 1
```

#### 실행결과

```python
4
```

<br>

### ⌨️ 문제 풀이

1.  `m * n` 크기의 맵을 만들어 0으로 도배를 한 후, 쓰레기가 있는 곳의 좌표를 받아 1이라고 표시했다.  
    쓰레기가 있는 좌표는 따로 `foot_t`라는 변수에 담았다.
2.  `food_t` 를 순회하면서 어느 좌표에서 가장 쓰레기가 크게 되는지 깊이 우선 탐색을 통해 계산해준다.

<br>

### 🖥 소스 코드

```python
from sys import stdin, setrecursionlimit
setrecursionlimit(10 ** 9)

n, m, k = map(int, stdin.readline().split())
arr = [[0] * (m + 1) for _ in range(n + 1)]
food_t = []

for _ in range(k):
    x, y = map(int, stdin.readline().split())
    arr[x][y] = 1
    food_t.append((x, y))

answer = -1e9
dx, dy = [1, -1, 0, 0], [0, 0, -1, 1]


def dfs(x, y):
    global res
    if x < 0 or y < 0 or x > n or y > m:
        return

    if arr[x][y] == 1:
        arr[x][y] = 0
        res += 1
        for i in range(4):
            dfs(x + dx[i], y + dy[i])

        return


for x, y in food_t:
    res = 0
    dfs(x, y)
    answer = max(res, answer)

print(answer)
```

<br>

### 💾 느낀점

1.  recursive 제약이 있어, `setrecursionlimit` 함수를 사용한다는 것을 매일 까먹는다. 조심해야겠다.
2.  DFS로 한번, BFS로 한번 풀어보았다. 이런 문제가 가장 싫었었는데 지금은 가장 좋다.