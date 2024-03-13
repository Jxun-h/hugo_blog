---
author: ["Jxun-h"]
title: "[BOJ] 16935 배열 돌리기 3 with Python"
date: "2022-03-04"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/16935" target="_blank">BOJ 16935 배열 돌리기 3</a>

<br>

### 💡 조건

1.  크기가 N×M인 배열이 있을 때, 배열에 연산을 R번 적용하려고 한다.  
    1번 연산은 배열을 상하 반전시키는 연산이다.  
    2번 연산은 배열을 좌우 반전시키는 연산이다.  
    3번 연산은 오른쪽으로 90도 회전시키는 연산이다.  
    4번 연산은 왼쪽으로 90도 회전시키는 연산이다.  
    **5, 6번은 문제 참고**
2.  첫째 줄에 배열의 크기 N, M과 수행해야 하는 연산의 수 R이 주어진다.  
    2 ≤ N, M ≤ 100, N, M은 짝수  
    1 ≤ R ≤ 1,000
3.  둘째 줄부터 N개의 줄에 배열 A의 원소 Aij가 주어진다.  
    1 ≤ Aij ≤ 108
4.  연산은 공백으로 구분되어져 있고, 문제에서 설명한 연산 번호이며, 순서대로 적용시켜야 한다.
5.  **구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
6 8 6
3 2 6 3 1 2 9 7
9 7 8 2 1 4 5 3
5 9 2 1 9 6 1 8
2 1 3 8 6 3 9 2
1 3 2 8 7 9 2 1
4 5 1 9 8 2 1 3
1 2 3 4 5 6
```

#### 실행결과

```py
3 1 2 8 9 1 5 4
1 2 9 7 8 2 3 1
2 9 3 6 8 3 1 2
8 1 6 9 1 2 9 5
3 5 4 1 2 8 7 9
7 9 2 1 3 6 2 3
```

<br>

### ⌨️ 문제 풀이

1.  말 그대로 구현을 하는 문제였다.


<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m, r = map(int, stdin.readline().split())
board = []
for _ in range(n):
    board.append(list(map(int, stdin.readline().split())))

command = list(map(int, list(stdin.readline().split())))
for i in range(r):
    if command[i] == 1:
        length = len(board)
        for j in range(length // 2):
            board[j], board[length - 1 - j] = board[length - 1 - j], board[j]

    elif command[i] == 2:
        for i in range(len(board)):
            board[i] = list(reversed(board[i]))

    elif command[i] == 3:
        if len(board) == n:
            new_board = [[0] * n for _ in range(m)]
            for j in range(m):
                for k in range(n):
                    new_board[j][n - 1 - k] = board[k][j]
        else:
            new_board = [[0] * m for _ in range(n)]
            for j in range(n):
                for k in range(m):
                    new_board[j][m - 1 - k] = board[k][j]

        board = new_board

    elif command[i] == 4:
        if len(board) == n:
            new_board = [[0] * n for _ in range(m)]
            for j in range(m - 1, -1, -1):
                for k in range(n - 1, -1, -1):
                    new_board[(m - 1) - j][k] = board[k][j]
        else:
            new_board = [[0] * m for _ in range(n)]
            for j in range(n - 1, -1, -1):
                for k in range(m - 1, -1, -1):
                    new_board[(n - 1) - j][k] = board[k][j]

        board = new_board

    elif command[i] == 5:
        r, c = len(board), len(board[0])
        new_board = [[0] * c for _ in range(r)]

        arr1 = [item[:c // 2] for item in board[:r // 2]]
        arr2 = [item[c // 2:] for item in board[:r // 2]]
        arr3 = [item[c // 2:] for item in board[r // 2:]]
        arr4 = [item[:c // 2] for item in board[r // 2:]]

        for j in range(r // 2):
            new_board[j] = arr4[j] + arr1[j]

        for j in range(r // 2, r):
            new_board[j] = arr3[j - r // 2] + arr2[j - r // 2]
        board = new_board

    elif command[i] == 6:
        r, c = len(board), len(board[0])
        new_board = [[0] * c for _ in range(r)]

        arr1 = [item[:c // 2] for item in board[:r // 2]]
        arr2 = [item[c // 2:] for item in board[:r // 2]]
        arr3 = [item[c // 2:] for item in board[r // 2:]]
        arr4 = [item[:c // 2] for item in board[r // 2:]]
        for j in range(r // 2):
            new_board[j] = arr2[j] + arr3[j]

        for j in range(r // 2, r):
            new_board[j] = arr1[j - r // 2] + arr4[j - r // 2]
        board = new_board

for arr in board:
    print(*arr)
```

<br>

### 💾 느낀점

1.  배열을 돌리는게 꽤 까다롭긴한데, 천천히 그림을 그리며 정리해서 풀었습니다.