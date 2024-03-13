---
author: ["Jxun-h"]
title: "[BOJ] 16956 늑대와 양 with Python"
date: "2022-07-02"
description: ""
summary: ""
tags: ["자료구조", "PS", "애드혹", "구성적", "그래프 이론", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/16956" target="_blank">BOJ 16956 늑대와 양</a>

<br>

### 💡 조건

1.  크기가 R×C인 목장이 있고, 목장은 1×1 크기의 칸으로 나누어져 있다.

2.  각각의 칸에는 비어있거나, 양 또는 늑대가 있다. 양은 이동하지 않고 위치를 지키고 있고, 늑대는 인접한 칸을 자유롭게 이동할 수 있다.  
    두 칸이 인접하다는 것은 두 칸이 변을 공유하는 경우이다.

3.  목장에 울타리를 설치해 늑대가 양이 있는 칸으로 갈 수 없게 하려고 한다.  
    늑대는 울타리가 있는 칸으로는 이동할 수 없다. 울타리를 설치해보자.

4.  목장의 크기 R, C가 주어진다.  
    R개의 줄에 목장의 상태가 주어진다. '.'는 빈 칸, 'S'는 양, 'W'는 늑대이다.  
    1 ≤ R, C ≤ 500

5.  늑대가 양이 있는 칸으로 갈 수 없게 할 수 있다면 첫째 줄에 1을 출력하고, 둘째 줄부터 R개의 줄에 목장의 상태를 출력한다.  
    울타리는 'D'로 출력한다. 울타리를 어떻게 설치해도 늑대가 양이 있는 칸으로 갈 수 있다면 첫째 줄에 0을 출력한다.  
    **이 문제는 설치해야 하는 울타리의 최소 개수를 구하는 문제가 아니다.**

6.  **애드 혹, 구성적, 그래프 이론** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
5 5
.S...
...S.
S....
...S.
.S...
```

#### 실행결과 1

```py
1
.S...
...S.
S.D..
...S.
.S...
```

#### 예제 2

```py
1 2
SW
```

#### 실행결과 2

```py
0
```

<br>

### ⌨️ 문제 풀이

1.  이 문제는 노트에 적혀있듯, 설치해야하는 최소 울타리 개수를 구하는 문제가 아니다.  
    울타리를 설치해서 늑대가 양에게 접근할 수 있는지에 대해서 알아보면 되는 문제이다.  
    그렇기 때문에, 늑대가 양에게 접근할 수 있다면 0, 없다면 1을 출력하고

2.  **최소 몇 개의 울타리를 설치해야하는지 알아보는 것이 아니기 때문**에, 울타리를 설치할 수 있는 모든 공간을 울타리로 바꿔준다.

3.  맵 정보를 입력받아 board에 입력할 때, 한 줄마다 문자 W 를 검색해 늑대의 좌표를 wolf 리스트에 저장해둔다.

4.  wolf 리스트를 순회하면서 해당 wolf 좌표에서 양에게 접근을 할 수 있으면 retrun False를 해주고 0을 출력해준 뒤, exit().

5.  return True 라면 1을 출력 후 board 상태를 출력해주면 된다.

<br>

### 🖥 소스 코드

```py
from collections import deque
from sys import stdin

r, c = map(int, stdin.readline().split())
board = []
wolf = []
dx, dy = [1, 0, 0, -1], [0, 1, -1, 0]
for i in range(r):
    data = list(stdin.readline().rstrip().replace('.', 'D'))
    board.append(data)
    for j in range(c):
        if data[j] == 'W':
            wolf.append((i, j))


def bfs(x, y):
    q = deque()
    q.append((x, y))
    visited = set()
    visited.add((x, y))

    while q:
        x, y = q.popleft()
        for i in range(4):
            nx, ny = x + dx[i], y + dy[i]
            if 0 <= nx < r and 0 <= ny < c:
                if (nx, ny) not in visited and board[nx][ny] != 'D' and board[nx][ny] != 'W':
                    if board[nx][ny] == 'S':
                        return False
                    else:
                        visited.add((nx, ny))
                        q.append((nx, ny))

    return True


for x, y in wolf:
    if not bfs(x, y):
        print(0)
        exit()

print(1)
for i in board:
    print(*i, sep='')
```

<br>

### 💾 느낀점

1.  가장 중요한 포인트는 **최소 몇 개의 울타리를 설치해야하는지 알아보는 것이 아니다** 라는 것에 중점을 두고 풀이해서 쉽게 풀 수 있었다.