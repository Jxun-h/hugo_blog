---
author: ["Jxun-h"]
title: "[BOJ] 17485 진우의 달 여행 (Large) with Python"
date: "2022-06-04"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "완전탐색", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/17485" target="_blank">BOJ 17485 진우의 달 여행 (Large)</a>

<br>

### 💡 조건

1.  지구와 우주사이는 N X M 행렬로 나타낼 수 있으며 각 원소의 값은 우주선이 그 공간을 지날 때 소모되는 연료의 양이다.  
    N, M (2 ≤ N, M ≤ 1000), 각 행렬의 원소값은 100 이하의 자연수이다.

<br>
<center><img src='/17485_1.png' style='filter:invert(100%);'></center>
<br>

2.  지구 -> 달로 가는 경우 우주선이 움직일 수 있는 방향은 아래와 같다.

<br>
<center><img src='/17485_2.png' style='filter:invert(100%);'></center>
<br>

3.  우주선은 전에 움직인 방향으로 움직일 수 없다. 즉, 같은 방향으로 두번 연속으로 움직일 수 없다.  
    진우의 목표는 연료를 최대한 아끼며 지구의 어느위치에서든 출발하여 달의 어느위치든 착륙하는 것이다.

4.  최대한 돈을 아끼고 살아서 달에 도착하고 싶은 진우를 위해 달에 도달하기 위해 필요한 연료의 최소값을 계산하는 문제

5.  **다이나믹 프로그래밍, 완전탐색** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
6 4
5 8 5 1
3 5 8 4
9 77 65 5
2 1 5 2
5 98 1 5
4 95 67 58
```

#### 실행결과

```py
29
```

<br>

### ⌨️ 문제 풀이

1.  완전 탐색과 다이나믹프로그래밍 알고리즘을 이용하여 문제를 해결한다.

2.  탐색한 경로를 다시 탐색하지 않는다는 아이디어를 위해서 메모이제이션을 사용한다.  
    각 공간을 지날 때 최솟값을 기록하고 이전의 값을 사용하는 방식을 사용하면 된다.

3.  재귀 함수를 사용하여 풀이한다면 점화식을 만들어볼 수 있다.
    
    ```py
    dp[r][c][cur_dir] = min(dp[r][c][cur_dir], recursive_find(next_r, next_c), next_dir) + board[r][c])
    ```
    

4.  (3)번에서 도출한 점화식을 통해서 최솟값을 반영해 불필요한 탐색을 막을 수 있다.

5.  PyPy3 로 제출해야 시간초과가 걸리지 않는다.

6.  setrecursionlimit 을 사용해야 런타임 에러 발생을 방지한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin, setrecursionlimit

setrecursionlimit(2000)


def visit_tf(pos, cur_direction, next_direction):
    x, y = pos
    return cur_direction != next_direction and 0 <= y < m


def solve(pos, cur_pos):
    x, y = pos
    if x == n:
        return 0

    if dp[x][y][cur_pos] != int(1e9):
        return dp[x][y][cur_pos]

    for next_pos, dy in enumerate(direction):
        npx, npy = x + 1, y + dy
        if visit_tf((npx, npy), cur_pos, next_pos):
            data = solve((npx, npy), next_pos) + arr[x][y]
            dp[x][y][cur_pos] = min(data, dp[x][y][cur_pos])

    return dp[x][y][cur_pos]


if __name__ == '__main__':
    n, m = map(int, stdin.readline().split())
    arr = []
    answer = int(1e9)
    dp = [[[answer] * 3 for i in range(m)] for _ in range(n)]

    direction = [-1, 0, 1]

    for _ in range(n):
        arr.append(list(map(int, stdin.readline().split())))

    for i in range(m):
        for j in range(3):
            answer = min(answer, solve((0, i), j))

    print(answer)
```

<br>

### 💾 느낀점

1.  스스로 풀이하지 못해 블로그 글을 참고하여 풀이했다.