---
author: ["Jxun-h"]
title: "[BOJ] 1520 내리막 길 with Python"
date: "2022-06-10"
description: ""
summary: ""
tags: ["자료구조", "PS", "DFS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1520" target="_blank">BOJ 1520 내리막 길</a>

<br>

### 💡 조건

1.  지도는 아래 그림과 같이 직사각형 모양이며 여러 칸으로 나뉘어져 있다.  
    한 칸은 한 지점을 나타내는데 각 칸에는 그 지점의 높이가 쓰여 있으며, 각 지점 사이의 이동은 지도에서 상하좌우 이웃한 곳끼리만 가능하다.

2.  현재 제일 왼쪽 위 칸이 나타내는 지점에 있는 세준이는 제일 오른쪽 아래 칸이 나타내는 지점으로 가려고 한다.  
    그런데 가능한 힘을 적게 들이고 싶어 항상 높이가 더 낮은 지점으로만 이동하여 목표 지점까지 가고자 한다.  
    위와 같은 지도에서는 다음과 같은 세 가지 경로가 가능하다.

3.  지도가 주어질 때 이와 같이 제일 왼쪽 위 지점에서 출발하여 제일 오른쪽 아래 지점까지  
    항상 내리막길로만 이동하는 경로의 개수를 구하는 프로그램을 작성하시오.

4.  첫째 줄에는 지도의 세로의 크기 M과 가로의 크기 N이 빈칸을 사이에 두고 주어진다.  
    이어 다음 M개 줄에 걸쳐 한 줄에 N개씩 위에서부터 차례로 각 지점의 높이가 빈 칸을 사이에 두고 주어진다.  
    M과 N은 각각 500이하의 자연수이고, 각 지점의 높이는 10000이하의 자연수이다.

5.  첫째 줄에 이동 가능한 경로의 수 H를 출력한다. 모든 입력에 대하여 H는 10억 이하의 음이 아닌 정수이다.

6.  **DFS, DP** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4 5
50 45 37 32 30
35 50 40 20 25
30 30 25 17 28
27 24 22 15 10
```

#### 실행결과

```py
3
```

<br>

### ⌨️ 문제 풀이

1.  제일 오른쪽 아래지점은 DP[N][M] 에서, DP[N - 1][M] + DP[N][M - 1] 이다.

2.  (0, 0)부터 시작하여 DFS로 진행을 하면서 갈 수 있는 경로에 대해서 계산한다.

3.  DP에는 경우의 수를 저장하면서 진행하면 되는데, 문제에서 나왔듯이, 입력받은 board 에서 현재 위치한 위치의 값보다  
    적어야 움직일 수 있기 때문에 DFS 함수를 코딩할 때 조건문이 필요하다.

4.  만약 방문이 되지 않은 곳이라면 DP 리스트에 -1로 표현될 수 있게 DP 리스트를 -1 로 모두 채워서 구현한다.  
    현재 방문한 좌표가 방문을 이미 했던 곳이라면 바로 현재 좌표의 DP 리스트를 return 한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin, setrecursionlimit
setrecursionlimit(10 ** 6)

n, m = map(int, stdin.readline().split())
board = []
for _ in range(n):
    board.append(list(map(int, stdin.readline().split())))

dp = [[-1] * m for _ in range(n)]
dx, dy = [1, 0, 0, -1], [0, -1, 1, 0]


def solve(x, y):
    global ans

    if (x, y) == (n - 1, m - 1):
        return 1

    if dp[x][y] != -1:
        return dp[x][y]

    dp[x][y] = 0

    for i in range(4):
        nx, ny = x + dx[i], y + dy[i]
        if 0 <= nx < n and 0 <= ny < m:
            if board[x][y] > board[nx][ny]:
                dp[x][y] += solve(nx, ny)

    return dp[x][y]


print(solve(0, 0))
```
