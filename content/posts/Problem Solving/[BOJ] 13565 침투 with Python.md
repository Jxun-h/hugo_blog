---
author: ["Jxun-h"]
title: "[BOJ] 13565 침투 with Python"
date: "2022-02-19"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "그래프 이론", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/13565" target="_blank">BOJ 13565 침투</a>

<br>

### 💡 조건

1.  격자의 크기를 나타내는 M (2 ≤ M ≤ 1,000) 과 N (2 ≤ N ≤ 1,000)
2.  M줄에 걸쳐서, N개의 0 또는 1 이 공백 없이 주어진다. 0은 전류가 잘 통하는 흰색, 1은 전류가 통하지 않는 검은색 격자임을 뜻한다.
3.  맨 윗줄에서 받은 전기가 맨 밑 줄까지 갈 수 있다면 True, 아니면 False
4.  **BFS** 유형의 문제

### 🔖 예제 및 실행결과

#### 예제

```py
5 6
010101
010000
011101
100011
001011
```

#### 실행결과

```py
NO
```

<br>

### ⌨️ 문제 풀이

1.  전류판을 board 리스트에 입력받아 저장합니다.  
    방문처리를 할 visited 를 set() 자료형으로 생성합니다.
2.  bfs 함수는 너비우선탐색의 로직을 기본적으로만 구현한 형태입니다.  
    상하좌우로 움직이면서 큐에 다음 이동할 좌표를 넣으며, 이동할 수 있는 좌표를 큐에 넣었을 땐 visited 에 넣어줍니다.  
    만약 n - 1 과 현재 큐에서 뽑은 x 좌표의 값이 같다면 맨 밑으로 전류가 전달 된 것이니 true 를 반환합니다.  
    아니라면 None 이 반환됩니다.
3.  가장 윗줄을 볼 것이기 때문에 m만큼 순회를 시작합니다.(j)  
    borad[0][i] 가 0이고 (0, j) 좌표가 이미 검사한 좌표가 아니라면 bfs에 넣습니다.
4.  bfs의 결과 값이 true가 반환되었다면 res_tf 를 true로 갱신하고 순회를 종료합니다.
5.  res_tf 가 true 라면 YES, 아니라면 NO 를 출력합니다


<br>

### 🖥 소스 코드

```py
from sys import stdin
from collections import deque

n, m = map(int, stdin.readline().split())
board = []
visited = set()
for _ in range(n):
    board.append(list(map(int, list(stdin.readline().rstrip()))))

dx, dy = [0, 0, -1, 1], [1, -1, 0, 0]
res_tf = False


def bfs(x, y):
    q = deque()
    q.append((x, y))
    visited.add((x, y))

    while q:
        x, y = q.popleft()
        if x == n - 1:
            return True

        for i in range(4):
            nx, ny = dx[i] + x, dy[i] + y
            if -1 < nx < n and -1 < ny < m and (nx, ny) not in visited:
                if board[nx][ny] == 0:
                    q.append((nx, ny))
                    visited.add((nx, ny))


for j in range(m):
    if board[0][j] == 0 and (0, j) not in visited:
        if bfs(0, j) is True:
            res_tf = True
            break

print('YES') if res_tf else print('NO')
```

<br>

### 💾 느낀점

1.  간단한 너비우선탐색의 문제였습니다.