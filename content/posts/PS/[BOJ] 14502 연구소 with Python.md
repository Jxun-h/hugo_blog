---
author: ["Jxun-h"]
title: "[BOJ] 14502 연구소 with Python"
date: "2022-01-24"
description: ""
summary: ""
tags: ["자료구조", "PS", "DFS", "BFS", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/14502" target="_blank">BOJ 14502 연구소</a>

<br>

### 💡 조건

1.  연구소는 크기가 N×M인 직사각형으로 나타낼 수 있으며, 직사각형은 1×1 크기의 정사각형으로 나누어져 있다.
2.  새로 세울 수 있는 벽의 개수는 3개이며, 꼭 3개를 세워야 한다.
3.  벽을 3개 세운 뒤, 바이러스가 퍼질 수 없는 곳을 안전 영역이라고 한다.
4.  지도의 세로 크기 N과 가로 크기 M이 주어진다. (3 ≤ N, M ≤ 8)
5.  0은 빈 칸, 1은 벽, 2는 바이러스가 있는 위치이다. 2의 개수는 2보다 크거나 같고, 10보다 작거나 같은 자연수이다.
6.  **DFS + BFS, 브루트포스 알고리즘 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
7 7
2 0 0 0 1 1 0
0 0 1 0 1 2 0
0 1 1 0 1 0 0
0 1 0 0 0 0 0
0 0 0 0 0 1 1
0 1 0 0 0 0 0
0 1 0 0 0 0 0
```

#### 실행결과

```py
27
```

<br>

### ⌨️ 문제 풀이

1.  맵의 정보를 입력받으면서, 바이러스의 위치를 virus_xy 리스트에 저장한다.
2.  안전 영역의 최댓값을 담을 변수 score 를 -int(1e9)로 초기화한다.
3.  이 문제의 풀이를 위해서 사용할 함수는 총 3개이다.
    -   get_score(board) : 안전 영역의 크기를 계산하여 최댓값일 경우 score 갱신
    -   insfection(x, y, board) : 벽을 세우고, 바이러스가 이동하며 감염. 보드를 갱신. BFS 알고리즘을 사용.
    -   solutions(cnt) : 3개의 벽을 세울 수 있게 cnt를 파라미터로 사용. DFS 알고리즘을 사용.
4.  설치한 벽의 개수가 3개가 될 때까지 DFS 알고리즘을 사용해 맵을 갱신한다.  
    벽이 3개가 설치 되었다면, 새로운 보드를 만들고 감염을 시켜준다.
5.  새로운 보드를 감염시킨 후, score 계산을 한다.  
    계산한 score 값이 최댓값일 경우, 갱신한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from collections import deque

n, m = map(int, stdin.readline().split())
board = []
virus_xy = []

for i in range(n):
    data = list(map(int, stdin.readline().split()))
    board.append(data)
    for j in range(len(data)):
        if data[j] == 2:
            virus_xy.append((i, j))

score = -1e9
dx, dy = [1, 0, 0, -1], [0, 1, -1, 0]


def get_score(board):
    global score
    cnt = 0
    for x in range(n):
        for y in range(m):
            if board[x][y] == 0:
                cnt += 1

    score = max(score, cnt)


def insfection(x, y, board):
    q = deque()
    q.append((x, y))

    while q:
        a, b = q.popleft()
        for i in range(4):
            nx, ny = a + dx[i], b + dy[i]
            if -1 < nx < n and -1 < ny < m:
                if board[nx][ny] == 0:
                    board[nx][ny] = 2
                    q.append((nx, ny))


def solutions(cnt):
    if cnt == 3:
        new_board = [item[:] for item in board]
        for x, y in virus_xy:
            insfection(x, y, new_board)
        get_score(new_board)

    else:
        for x in range(n):
            for y in range(m):
                if board[x][y] == 0:
                    board[x][y] = 1
                    cnt += 1
                    solutions(cnt)
                    cnt -= 1
                    board[x][y] = 0


solutions(0)
print(score)
```

<br>

### 💾 느낀점

1.  PyPy3 로 채점하여 통과했다.
2.  DFS를 사용하여 벽을 3개 설치한 후, BFS를 사용하여 감염, score 계산하는 로직을 이해하는 것이 처음엔 어려웠다.
3.  문제를 풀고서 매우 뒤늦게 블로그 포스팅을 하는 것인데, 로직을 이해하니 비슷한 유형의 문제를 푸는 것이 확실히 수월해졌다.
4.  여기서 조금 더 응용을 하자면, 벽을 설치했는지 안했는지의 state를 저장할  
    dp 배열을 만들면 메모리제이션을 통해 시간복잡도를 줄일 수 있는 유사문제도 있었다.