---
author: ["Jxun-h"]
title: "[BOJ] 4179 불! with Python"
date: "2021-08-28"
description: ""
summary: ""
tags: ["DP", "PS", "다이나믹프로그래밍", "알고리즘"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---
<br>

## 📌 [BOJ 4179 불!](https://www.acmicpc.net/problem/4179)
<br>

### 💡 조건 및 풀이

1.  `R * C` 크기의 배열을 입력받아 지훈이가 미로에서 탈출 할 수 있는지 구하는 문제.
2.  `R * C` 크기의 배열은 최대 `1000 * 1000`
3.  **BFS 유형의 문제**
4.  미로의 벽에 붙어있으면 탈출이 가능하다.
5.  **불을 먼저 지른 후, 지훈이의 이동 가능 경로를 살핀다.**
6.  **방문처리를 통해 한 번 갔던 곳은 다시 가지 않는다.**

<br>

### 🔖 예제 및 실행결과

#### 예제

```
4 4
####
#JF#
#..#
#..#
```

#### 실행결과
```
3
```

<br>

### ⌨️ 문제 풀이

1.  과정방문처리용 리스트를 만들어 사용하니 시간초과와 메모리 초과가 떴다.
2.  임시 배열을 만들어 불과 지훈이가 움직일 때 이동 가능한 경로를 모두 넣어주고 while 문이 종료되었을 때 큐에 삽입
3.  지훈이가 지나간 곳은 `'$'`로 변경
4.  불은 `'$'` 와 `'.'` 를, 지훈이는 오로지 `'.'` 만 갈 수 있게 처리.
5.  지훈이가 움직일 때, Queue 에서 현재 지훈이의 좌표를 뽑아, 벽에 위치하고 있다면 탈출 성공.
6.  `if x == 0 or y == 0 or x == r - 1 or y == c - 1:`
7.  더 이상 지훈이가 움직일 경로가 없다면 탈출 실패
8.  `if not J:`

<br>

### 🖥 소스 코드

```python
from sys import stdin
from collections import deque

dx, dy = [1, -1, 0, 0], [0, 0, 1, -1]
r, c = map(int, stdin.readline().split())
board, res = [], 0

# 지환이와 불난 곳 저장할 변수
F, J = deque(), deque()

for i in range(r):
    data = list(stdin.readline().rstrip())
    for j in range(c):
        if data[j] == 'J':
            J.append((i, j))
        if data[j] == 'F':
            F.append((i, j))

    board.append(data)


def bfs():
    global F, J, res

    while 1:
        res += 1
        temp = []
        while F:
            x, y = F.popleft()
            for i in range(4):
                nx, ny = x + dx[i], y + dy[i]
                if -1 < nx < r and -1 < ny < c:
                    if board[nx][ny] == '.' or board[nx][ny] == '$':
                        temp.append((nx, ny))
                        board[nx][ny] = 'F'
        F = deque(temp)

        temp = []
        while J:
            x, y = J.popleft()
            if x == 0 or y == 0 or x == r - 1 or y == c - 1:
                return res

            for i in range(4):
                nx, ny = dx[i] + x, dy[i] + y
                if -1 < nx < r and -1 < ny < c and board[nx][ny] == '.':
                    temp.append((nx, ny))
                    board[x][y] = '$'
                    board[nx][ny] = 'J'

        J = deque(temp)
        if not J:
            return False


if bfs():
    print(res)
else:
    print('IMPOSSIBLE')
```
<br>


### 💾 느낀점

- BFS 유형 문제에서 난이도가 실버2 ~ 골드4 로만 올라가도 헤매는 모습을 보였다.
- 방문처리용 배열의 다양한 사용법을 눈에 익히고 응용할 줄 알아야겠다.
- 방문처리용 배열을 사용하기 전, 메모리 초과가 뜰 각인지 잴 줄 알아야겠다.
- 문제를 나름대로 해석하고 압축하는 능력을 더 키워야겠다.