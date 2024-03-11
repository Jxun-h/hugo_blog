---
author: ["Jxun-h"]
title: "[Programmers] 블록 이동하기 with Python"
date: "2021-12-12"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "시뮬레이션", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["Programmers"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/60063" target="_blank">Programmers 블록 이동하기 with Python</a>

<br>

### 💡 조건

1.  `board`의 한 변의 길이는 `5 이상 100 이하`.  
    `board`의 원소는 `0(이동가능 블록)` 또는 `1(이동불가 벽)`.
2.  로봇이 처음에 놓여 있는 칸 `(1, 1), (1, 2)`는 항상 0으로 주어진다.
3.  로봇은 회전할 수 있다.
4.  **BFS, 시뮬레이션**의 문제
5.  `(N, N)` 좌표까지 도달하는 최소시간을 구하는 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
print(solution([[0, 0, 0, 1, 1],[0, 0, 0, 1, 0],[0, 1, 0, 1, 1],[1, 1, 0, 0, 1],[0, 0, 0, 0, 0]]))
```

#### 실행결과

```python
7
```

<br>

### 🖥 소스 코드

```python
from collections import deque


def get_next_pos(pos, board):
    next_pos = []

    pos = list(pos)
    pos1_x, pos1_y, pos2_x, pos2_y = pos[0][0], pos[0][1], pos[1][0], pos[1][1]

    dx = [-1, 1, 0, 0]
    dy = [0, 0, -1, 1]

    for i in range(4):
        pos1_next_x, pos1_next_y, pos2_next_x, pos2_next_y = pos1_x + dx[i], pos1_y + dy[i], pos2_x + dx[i], pos2_y + dy[i]

        if board[pos1_next_x][pos1_next_y] == 0 and board[pos2_next_x][pos2_next_y] == 0:
            next_pos.append({(pos1_next_x, pos1_next_y), (pos2_next_x, pos2_next_y)})

    if pos1_x == pos2_x:
        for i in [-1, 1]:

            if board[pos1_x + i][pos1_y] == 0 and board[pos2_x + i][pos2_y] == 0:
                next_pos.append({(pos1_x, pos1_y), (pos1_x + i, pos1_y)})
                next_pos.append({(pos2_x, pos2_y), (pos2_x + i, pos2_y)})

    elif pos1_y == pos2_y:
        for i in [-1, 1]:
            if board[pos1_x][pos1_y + i] == 0 and board[pos2_x][pos2_y + i] == 0:
                next_pos.append({(pos1_x, pos1_y), (pos1_x, pos1_y + i)})
                next_pos.append({(pos2_x, pos2_y), (pos2_x, pos2_y + i)})
    return next_pos


def solution(board):
    n = len(board)
    new_board = [[1] * (n + 2) for _ in range(n + 2)]
    for i in range(n):
        for j in range(n):
            new_board[i + 1][j + 1] = board[i][j]

    q = deque()
    visited = []

    pos = {(1, 1), (1, 2)}

    q.append((pos, 0))
    visited.append(pos)

    while q:
        pos, cost = q.popleft()

        if (n, n) in pos:
            return cost

        for next_pos in get_next_pos(pos, new_board):
            if next_pos not in visited:
                q.append((next_pos, cost + 1))
                visited.append(next_pos)
    return 0
```

<br>

### ⌨️ 문제 풀이

1.  가장 먼저, `(n * n)` 크기의 맵을 `(n + 2) * (n + 2)` 맵으로 새로 만들어  
    **맵 주변을 1로 둘러주어 이동하지 못하는 곳을 확실히 만들어준다.**
2.  시작 위치는 `{(1, 1), (1, 2)}` 로 `pos`에 저장한 뒤 큐에 넣는다.  
    물론 방문한 기록을 남길 `visited` 리스트에도 저장한다.
3.  BFS의 방식으로 `Queue`가 빌 때까지 순회를 한다.  
    단, 현재 위치에서 이동이 가능하거나 회전이 가능한 위치를 큐에 저장한다.
4.  3번에서 말한 이동 및 회전이 가능한 좌표는 함수 `get_next_pos()`에서 반환하는 좌표값들을 기준으로 한다.
5.  `get_next_pos` 에서는 현재 위치에서 이동 및 가능한 좌표를 반환하는데, 아래의 조건을 잘 확인해야한다.
    1.  상하좌우 네 방향으로 이동이 가능한지
    2.  현재 로봇이 가로로 놓여져 있는 경우 회전이 가능한지
    3.  현재 로봇이 세로로 놓여져 있는 경우 회전이 가능한지
6.  `get_next_pos` 에서 반환받은 좌표들 중, 이미 방문한 장소가 아니라면 방문처리를 하고 `cost(걸린 시간)` 을 큐와 함께 넣어준다.

<br>

### 💾 느낀점

1.  로봇이 90도 회전하는 좌표에 대해서 처리하고 반환하는 것이 어려웠다.
2.  좌표 계산이 헷갈려 힘이 들었다.
3.  좌표 및 인덱싱에 대해 연습이 많이 필요할 것 같다.