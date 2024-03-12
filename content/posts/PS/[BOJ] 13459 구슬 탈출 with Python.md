---
author: ["Jxun-h"]
title: "[BOJ] 13459 구슬 탈출 with Python"
date: "2022-06-03"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/13459" target="_blank">BOJ 13459 구슬 탈출</a>

<br>

### 💡 조건

1.  구슬 탈출은 직사각형 보드에 빨간 구슬과 파란 구슬을 하나씩 넣은 다음, 빨간 구슬을 구멍을 통해 빼내는 게임이다.

2.  보드의 세로 크기는 N, 가로 크기는 M이고, 편의상 1×1크기의 칸으로 나누어져 있다.  
    N, M (3 ≤ N, M ≤ 10)

3.  가장 바깥 행과 열은 모두 막혀져 있고, 보드에는 구멍이 하나 있다.  
    빨간 구슬과 파란 구슬의 크기는 보드에서 1×1크기의 칸을 가득 채우는 사이즈이고, 각각 하나씩 들어가 있다.  
    게임의 목표는 빨간 구슬을 구멍을 통해서 빼내는 것이다. 이때, 파란 구슬이 구멍에 들어가면 안 된다.

4.  왼쪽으로 기울이기, 오른쪽으로 기울이기, 위쪽으로 기울이기, 아래쪽으로 기울이기와 같은 네 가지 동작이 가능하다.

5.  각각의 동작에서 공은 동시에 움직인다. 빨간 구슬이 구멍에 빠지면 성공이지만, 파란 구슬이 구멍에 빠지면 실패이다.  
    빨간 구슬과 파란 구슬이 동시에 구멍에 빠져도 실패이다. 빨간 구슬과 파란 구슬은 동시에 같은 칸에 있을 수 없다.  
    빨간 구슬과 파란 구슬의 크기는 한 칸을 모두 차지한다. 기울이는 동작을 그만하는 것은 더 이상 구슬이 움직이지 않을 때 까지이다.

6.  보드의 상태가 주어졌을 때, 10번 이하로 빨간 구슬을 구멍을 통해 빼낼 수 있는지 구하는 문제.  
    파란 구슬을 구멍에 넣지 않으면서 빨간 구슬을 10번 이하로 움직여서 빼낼 수 있으면 1을 없으면 0을 출력한다.

7.  문자열은 '.', '#', 'O', 'R', 'B' 로 이루어져 있다.  
    '.'은 빈 칸을 의미하고, '#'은 공이 이동할 수 없는 장애물 또는 벽을 의미하며, 'O'는 구멍의 위치를 의미한다.  
    'R'은 빨간 구슬의 위치, 'B'는 파란 구슬의 위치이다.  
    입력되는 모든 보드의 가장자리에는 모두 '#'이 있다. 구멍의 개수는 한 개 이며, 빨간 구슬과 파란 구슬은 항상 1개가 주어진다.

7.  **BFS, 그래프탐색** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
10 10
##########
#R#...##B#
#...#.##.#
#####.##.#
#......#.#
#.######.#
#.#....#.#
#.#.##...#
#O..#....#
##########
```

#### 실행결과

```py
1
```

<br>

### ⌨️ 문제 풀이

1.  구슬을 네 개의 방향으로 기울였을 떄의 상태를 큐에 넣고 관리한다.

2.  이미 방문했던 곳에는 방문하지 않도록 visit 리스트에 방문처리를 해주어야 한다.

3.  큐에서 꺼내고, 이동을 시킬 좌표를 move 함수로 계산해 파란구슬이 '0'이 아니고 빨간 구슬이 '0'으로 갈 경우 1을 출력한다.

4.  만약 움직였을 때 두 구슬이 이동할 좌표가 '0' 이거나 10회를 초과하여 기울였다면 0을 출력한다.

<br>

### 🖥 소스 코드

```py
from collections import deque

n, m = map(int, input().split())
dx = [1, -1, 0, 0]
dy = [0, 0, -1, 1]
visit = [[[[False] * m for i in range(n)] for i in range(m)] for i in range(n)]
s = []


def move(i, j, dx, dy):
    c = 0
    while s[i + dx][j + dy] != "#" and s[i][j] != "O":
        i += dx
        j += dy
        c += 1
    return i, j, c


def bfs():
    while q:
        ri, rj, bi, bj, d = q.popleft()
        if d > 10:
            break
        for i in range(4):
            nri, nrj, rc = move(ri, rj, dx[i], dy[i])
            nbi, nbj, bc = move(bi, bj, dx[i], dy[i])
            if s[nbi][nbj] != "O":
                if s[nri][nrj] == "O":
                    print(1)
                    return
                if nri == nbi and nrj == nbj:
                    if rc > bc:
                        nri -= dx[i]
                        nrj -= dy[i]
                    else:
                        nbi -= dx[i]
                        nbj -= dy[i]
                if not visit[nri][nrj][nbi][nbj]:
                    visit[nri][nrj][nbi][nbj] = True
                    q.append([nri, nrj, nbi, nbj, d + 1])
    print(0)


for i in range(n):
    a = list(input())
    s.append(a)
    for j in range(m):
        if a[j] == "R":
            ri, rj = i, j
        if a[j] == "B":
            bi, bj = i, j

q = deque()
q.append([ri, rj, bi, bj, 1])
visit[ri][rj][bi][bj] = True

bfs()
```

<br>

### 💾 느낀점

1.  구슬을 움직여 상태를 나타내고, 방문처리를 할 리스트를 만들어 관리하는 것이 아이디어는 쉬웠다.

2.  구현이 어려웠다.