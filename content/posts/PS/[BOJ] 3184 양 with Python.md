---
author: ["Jxun-h"]
title: "[BOJ] 3184 양 with Python"
date: "2021-10-19"
description: ""
summary: ""
tags: ["너비우선탐색", "PS", "BFS", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/3184" target="_blank">BOJ 3184 양</a>

<br>

### 💡 조건

1.  `R`과 `C`가 주어지며`(3 ≤ R, C ≤ 250)`, 각 수는 마당의 행과 열의 수를 의미한다.  
    `R`개의 줄은 `C`개의 글자를 가진다. 이들은 마당의 구조(**울타리, 양, 늑대의 위치**)를 의미한다.
2.  글자 `'.' (점)`은 빈 필드를 의미하며, 글자 `'#'는 울타리`를, `'o'는 양`, `'v'는 늑대`를 의미한다.
3.  한 칸에서 수평, 수직만으로 이동할수 있다.  
    **영역 안의 양의 수가 늑대의 수보다 많다면 이기고, 늑대가 많으면 양은 사라진다.**
4.  **넓이 우선 탐색(BFS) 알고리즘 유형의 문제**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
6 6
...#..
.##v#.
#v.#.#
#.o#.#
.###.#
...###
```

#### 실행결과

```python
0 2
```

<br>

### ⌨️ 문제 풀이

1.  양과 늑대의 수를 담을 `answer` 리스트를 각각의 원소를 `0`으로 초기화하여 생성한다.  
    이미 방문했던 곳의 좌표를 담을 `set 자료형 visited`를 생성한다.
2.  이중 반복문으로 필드를 순회하면서, 다음 두가지에 해당하면 `BFS`를 수행한다.
    1.  `(i, j)` 가 `visited` 에 방문하지 않았을 때
    2.  `(i, j)` 에 해당하는 필드 값이 `v 혹은 o` 일 때
3.  `bfs 함수`에서 `vo`라는 `set()`이 두개 담긴 리스트를 생성해준다.  
    큐에는 `bfs` 를 수행하기 위해 받아온 `x, y` 값을 넣어주고, 큐가 빌 때까지 수행한다.
4.  큐에서 뽑아낸 `x, y` 좌표가 필드에서 양인지 늑대인지 구문하여 `vo[1] 혹은 v[0]` 에 저장해준다.  
    현재 좌표에서 상하좌우를 순회하며 방문하지 않았고, `#`이 아닌 필드의 좌표를 큐와 `visited` 에 넣어준다.
5.  큐가 비어 `while 반복문`이 종료되면, 양의 수와 늑대의 수를 비교하여  
    **수가 더 작은 쪽은 0으로, 큰 쪽은 숫자 그대로 반환한다.**
6.  bfs 함수에서 반환받은 값을 answer 원소에 각각 더해준다.

<br>

### 🖥 소스 코드

```python
from sys import stdin
from collections import deque

n, m = map(int, stdin.readline().split())
board = []
for n in range(n):
    board.append(list(stdin.readline().rstrip()))
dx, dy = [1, -1, 0, 0], [0, 0, -1, 1]
visited = set()


def bfs(x, y):
    vo = [set(), set()]
    q = deque()
    q.append((x, y))
    visited.add((x, y))
    while q:
        x, y = q.popleft()

        if board[x][y] == 'o':
            vo[1].add((x, y))
        elif board[x][y] == 'v':
            vo[0].add((x, y))

        for i in range(4):
            nx, ny = dx[i] + x, dy[i] + y
            if -1 < nx < n and -1 < ny < m:
                if board[nx][ny] != '#' and (nx, ny) not in visited:
                    q.append((nx, ny))
                    visited.add((nx, ny))

    if len(vo[0]) < len(vo[1]):
        return 0, len(vo[1])
    else:
        return len(vo[0]), 0


answer = [0, 0]
for i in range(n):
    for j in range(m):
        if (board[i][j] == 'v' or board[i][j] == 'o') and (i, j) not in visited:
            v, o = bfs(i, j)

            answer[0] += o
            answer[1] += v

print(*answer)
```

<br>

### 💾 느낀점

1.  BFS 문제였고, 쉽게 풀 수 있는 문제였다.
2.  다른 사람이 내 글을 보고 잘 이해할 수 있을지는 모르겠다.
3.  조금 더 쉽게 설명할 수 있게 더 높은 수준의 이해가 필요할 것 같다.