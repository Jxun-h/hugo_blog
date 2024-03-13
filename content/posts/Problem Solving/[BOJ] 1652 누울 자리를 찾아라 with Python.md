---
author: ["Jxun-h"]
title: "[BOJ] 1652 누울 자리를 찾아라 with Python"
date: "2023-04-03 16:40:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "문자열", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1652" target="_blank">BOJ 1652 누울 자리를 찾아라</a>

<br>

### 💡 조건

1.  코레스코 콘도에 있는 방은 NxN의 정사각형모양으로 생겼다.  
    방 안에는 옮길 수 없는 짐들이 이것저것 많이 있어서 영식이의 누울 자리를 차지하고 있었다.
2.  영식이가 누울 수 있는 자리에는 조건이 있다.  
    똑바로 연속해서 2칸 이상의 빈 칸이 존재하면 그 곳에 몸을 양 옆으로 쭉 뻗으면서 누울 수 있다.  
    가로로 누울 수도 있고 세로로 누울 수도 있다.
3.  **누울 때는 무조건 몸을 쭉 뻗기 때문에 반드시 벽이나 짐에 닿게 된다. (중간에 어정쩡하게 눕는 경우가 없다.)**
4.  방의 크기 N과 방의 구조가 주어졌을 때, 가로로 누울 수 있는 자리와 세로로 누울 수 있는 자리의 수를 구하는 문제
5.  N은 1이상 100이하의 정수이다. '.'은 아무것도 없는 곳을 의미하고, 'X'는 짐이 있는 곳을 의미한다.
6.  **구현, 문자열** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
5
....X
..XX.
.....
.XX..
X....
```

#### 실행결과 1

```py
5 4
```

<br>

### ⌨️ 문제 풀이

1.  가로, 세로로 누울 수 있는 자리에 대한 좌표값을 방문처리 리스트에 체크하여 여러번 카운팅 하지 않게 했다.
2.  이 문제에서 중요하게 생각해야할 점은, **누울 때는 무조건 몸을 쭉 뻗기 때문에 반드시 벽이나 짐에 닿게 된다.**  
    이다.
3.  누울 수 있는 자리를 방문처리 리스트에 체크할 때, 짐이 등장한다면 거기서 방문처리를 멈춰야한다.
4.  (3)번이 지켜지지 않을 경우, 극초반 테스트 케이스에서 **틀렸습니다** 가 나올 것이다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
board = []

for _ in range(n):
    board.append(list(stdin.readline().rstrip()))
g_v = [[1] * n for _ in range(n)]
s_v = [[1] * n for _ in range(n)]
g, s = 0, 0


def check(x, y, mode):
    global g, s

    if mode == 1:
        if board[x][y] == board[x][y + 1] and (g_v[x][y] == 1 and g_v[x][y + 1] == 1):
            g += 1
            for j in range(y, n):
                if board[x][j] == 'X':
                    break
                g_v[x][j] = 0
            for j in range(y, -1, -1):
                if board[x][j] == 'X':
                    break
                g_v[x][j] = 0

    elif mode == 2:
        if board[x][y] == board[x + 1][y] and (s_v[x][y] == 1 and s_v[x + 1][y] == 1):
            s += 1
            for i in range(x, n):
                if board[i][y] == 'X':
                    break
                s_v[i][y] = 0

            for i in range(x, -1, -1):
                if board[i][y] == 'X':
                    break
                s_v[i][y] = 0


for i in range(n):
    for j in range(n):
        if board[i][j] == '.':
            if j + 1 < n:
                check(i, j, 1)

            if i + 1 < n:
                check(i, j, 2)

print(g, s)
```