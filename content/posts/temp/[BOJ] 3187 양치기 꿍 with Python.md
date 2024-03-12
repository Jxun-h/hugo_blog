---
author: ["Jxun-h"]
title: "[BOJ] 3187 양치기 꿍 with Python"
date: "2022-03-14"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/3187" target="_blank">BOJ 3187 양치기 꿍</a>

<br>

### 💡 조건

1.  같은 울타리 영역 안의 양들의 숫자가 늑대의 숫자보다 더 많을 경우 늑대가 전부 잡아먹힌다. 물론 그 외의 경우는 양이 전부 잡아먹힌다.
2.  만약 빈 공간을 '.'(점)으로 나타내고 울타리를 '#', 늑대를 'v', 양을 'k'라고 나타낸다면 몇마리의 양과 늑대가 남아있는가?
3.  울타리로 막히지 않은 영역에는 양과 늑대가 없으며 양과 늑대는 대각선으로 이동할 수 없다.
4.  영역의 세로와 가로의 길이를 나타내는 두 개의 정수 R, C (3 ≤ R, C ≤ 250)
5.  **BFS** 유형의 문제

<br>

## 🔖 예제 및 실행결과

#### 예제

```py
6 6
...#..
.##v#.
#v.#.#
#.k#.#
.###.#
...###
```

#### 실행결과

```py
0 2
```

<br>

### ⌨️ 문제 풀이

1.  양과 늑대와 울타리 정보를 입력받아 board에 저장한다.
2.  맵을 순회하면서 울타리가 아니며, (i, j) 좌표가 방문하지 않은 좌표라면 bfs 함수를 호출한다.
3.  k일 때와 v일 때, .일 때 큐에 집어넣고, 방문처리를 해준다.
4.  k일 때는 sheep 변수에 1을 더하고, v일 때는 wolf 변수에 1을 더해준다.
5.  만약 늑대의 수가 많다면 wolf, 'w' 를 반환하고  
    만약 양의 수가 만ㄷ나면 sheep, 's' 을 반환한다.
6.  반환받은 결과에 따라서 양과 늑대의 수를 ans에 각각 저장한다.  
    ans는 앞부터 양과 늑대의 수다.

<br>

### 🖥 소스 코드

```py
from collections import deque
from sys import stdin

board = []
n, m = map(int, stdin.readline().split())
for i in range(n):
    board.append(list(stdin.readline().rstrip()))

dx, dy = [1, -1, 0, 0], [0, 0, 1, -1]
visited = set()


def bfs(x, y):
    wolf, sheep = 0, 0

    if board[x][y] == 'k':
        sheep += 1
    elif board[x][y] == 'v':
        wolf += 1

    q = deque()
    q.append((x, y))
    visited.add((x, y))

    while q:
        x, y = q.popleft()
        for i in range(4):
            nx, ny = dx[i] + x, dy[i] + y
            if -1 < nx < n and -1 < ny < m:
                if (nx, ny) not in visited:
                    if board[nx][ny] == 'k':
                        sheep += 1
                        q.append((nx, ny))
                        visited.add((nx, ny))

                    elif board[nx][ny] == 'v':
                        wolf += 1
                        q.append((nx, ny))
                        visited.add((nx, ny))

                    elif board[nx][ny] == '.':
                        q.append((nx, ny))
                        visited.add((nx, ny))

    if wolf >= sheep:
        return wolf, 'w'
    else:
        return sheep, 's'


ans = [0, 0]
for i in range(n):
    for j in range(m):
        if board[i][j] != '#' and (i, j) not in visited:
            res, win = bfs(i, j)
            if win == 's':
                ans[0] += res
            else:
                ans[1] += res

print(*ans)
```

<br>

### 💾 느낀점

1.  BSF를 사용하는 문제였습니다. 이와 같은 유형이 은근히 많아 연습하기 좋은 문제라고 생각합니다.