---
author: ["Jxun-h"]
title: "[BOJ] 2636 치즈 with Python"
date: "2022-03-18"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2636" target="_blank">BOJ 2636 치즈</a>

<br>

### 💡 조건

1.  정사각형 칸들로 이루어진 사각형 모양의 판이 있고, 그 위에 얇은 치즈가 놓여 있다.
2.  치즈를 공기 중에 놓으면 녹게 되는데 공기와 접촉된 칸은 한 시간이 지나면 녹아 없어진다.  
    치즈의 구멍 속에는 공기가 없지만 구멍을 둘러싼 치즈가 녹아서 구멍이 열리면 구멍 속으로 공기가 들어가게 된다.
3.  입력으로 사각형 모양의 판의 크기와 한 조각의 치즈가 판 위에 주어졌을 때,  
    공기 중에서 치즈가 모두 녹아 없어지는 데 걸리는 시간과 모두 녹기 한 시간 전에 남아있는 치즈조각이 놓여 있는 칸의 개수를 구하는 문제
4.  세로와 가로의 길이는 최대 100이다.
5.  치즈가 없는 칸은 0, 치즈가 있는 칸은 1로 주어지며 각 숫자 사이에는 빈칸이 하나씩 있다.
6.  **너비우선탐색, BFS** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
13 12
0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 1 1 0 0 0
0 1 1 1 0 0 0 1 1 0 0 0
0 1 1 1 1 1 1 0 0 0 0 0
0 1 1 1 1 1 0 1 1 0 0 0
0 1 1 1 1 0 0 1 1 0 0 0
0 0 1 1 0 0 0 1 1 0 0 0
0 0 1 1 1 1 1 1 1 0 0 0
0 0 1 1 1 1 1 1 1 0 0 0
0 0 1 1 1 1 1 1 1 0 0 0
0 0 1 1 1 1 1 1 1 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0
```

#### 실행결과

```py
3
5
```

<br>

### ⌨️ 문제 풀이

1.  BFS 알고리즘을 사용하여 좌표 이동을 하며 빈공간과 치즈를 입력받은 board 에서 치즈를 찾아 표시를 한 뒤, 녹았다고 처리하는 것이 목표입니다.  
    치즈가 모두 녹을 때까지 BFS 알고리즘을 호출해야하기에 while 로 호출해주면서 호출한 횟수를 ans에 저장해줍니다.
2.  이 문제는 치즈 위를 걷는 느낌이 아닌, 빈 공간을 걸으면서 치즈가 있는 곳을 표시하여 처리하는 문제입니다.
3.  (2)번과 같이 처리하지 않으면 치즈의 겉만 체크해줄 수 없습니다.
4.  체크된 치즈를 녹이는 함수인 melt() 를 정의하여 호출했습니다.
5.  melt() 함수를 호출하고 반환받은 값은 치즈가 녹은 개수입니다.  
    모두 녹기 한시간 전에 치즈가 녹은 개수를 출력해야하니, 반환된 값을 cnt 라는 변수에 저장해줍니다.
6.  녹지 않았다면 그대로 ans, cnt 를 출력해줍니다.

<br>

### 🖥 소스 코드

```py
from collections import deque
from sys import stdin

n, m = map(int, stdin.readline().split())
board = []
for _ in range(n):
    board.append(list(map(int, stdin.readline().split())))
dx, dy = [1, 0, 0, -1], [0, 1, -1, 0]
ans = 0
cnt = 0


def melt():
    cnt = 0
    for i in range(n):
        for j in range(m):
            if board[i][j] == -1:
                cnt += 1
                board[i][j] = 0
    return cnt


def bfs():
    global ans, cnt
    q = deque()
    q.append((0, 0))
    visited = set()
    visited.add((0, 0))
    while q:
        x, y = q.popleft()
        for i in range(4):
            nx, ny = dx[i] + x, dy[i] + y

            if -1 < nx < n and -1 < ny < m:
                if (nx, ny) not in visited:
                    if board[nx][ny] == 0:
                        q.append((nx, ny))
                        visited.add((nx, ny))
                    elif board[nx][ny] == 1:
                        board[nx][ny] = -1

    melt_cnt = melt()
    if melt_cnt != 0:
        cnt = melt_cnt
    else:
        print(ans)
        print(cnt)
        exit()


while 1:
    bfs()
    ans += 1
```

<br>

### 💾 느낀점

1.  빈공간을 걸으며 치즈의 벽면을 훑는다는 느낌을 얻기 어려웠다.