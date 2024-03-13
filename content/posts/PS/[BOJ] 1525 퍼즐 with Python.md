---
author: ["Jxun-h"]
title: "[BOJ] 1525 퍼즐 with Python"
date: "2022-06-14"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1525 퍼즐" target="_blank">BOJ 1525 퍼즐</a>

<br>

### 💡 조건

1.  3×3 표에 다음과 같이 수가 채워져 있다. 오른쪽 아래 가장 끝 칸은 비어 있는 칸이다.  
    ```
    1 2 3  
    4 5 6  
    7 8 9
    ```

2.  어떤 수와 인접해 있는 네 개의 칸 중에 하나가 비어 있으면, 수를 그 칸으로 이동시킬 수가 있다.  
    물론 표 바깥으로 나가는 경우는 불가능하다.  
    우리의 목표는 초기 상태가 주어졌을 때, 최소의 이동으로 위와 같은 정리된 상태를 만드는 것이다. 다음의 예를 보자.  
    ```
    1 3 9
    4 2 5  
    7 8 6
    ```
    ```
    1 2 3  
    4 5 9
    7 8 6
    ```

    ```
    1 2 3  
    4 5 9
    7 8 6
    ```

    ```
    1 2 3  
    4 5 6  
    7 8 9
    ```
    
3.  가장 윗 상태에서 세 번의 이동을 통해 정리된 상태를 만들 수 있다. 이와 같이 최소 이동 횟수를 구하는 프로그램을 작성하시오.

4.  세 줄에 걸쳐서 표에 채워져 있는 아홉 개의 수가 주어진다. 한 줄에 세 개의 수가 주어지며, 빈 칸은 0으로 나타낸다.

5.  첫째 줄에 최소의 이동 횟수를 출력한다. 이동이 불가능한 경우 -1을 출력한다.

6.  **BFS, 그래프탐색** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
1 0 3
4 2 5
7 8 6
```

#### 실행결과

```py
3
```

<br>

### ⌨️ 문제 풀이

1.  퍼즐의 숫자를 옮기면서 상태를 저장하고, 정렬된 상태가 확인되었으면 cnt를 리턴해준다.

2.  최소 이동 횟수를 출력해주려고 했으나, 이동을 하지 못하는 경우에는 -1를 출력한다.

<br>

### 🖥 소스 코드

```py
from collections import deque
from sys import stdin

arr = []
c = [1, 2, 3, 4, 5, 6, 7, 8, 0]
x, y = 0, 0
for i in range(3):
    data = list(map(int, stdin.readline().split()))
    arr.append(data)
    for j in range(3):
        if data[j] == 0:
            x, y = i, j

dx, dy = [1, 0, 0, -1], [0, 1, -1, 0]


def swap(a, b): return b, a


def solve(x, y):
    q = deque()
    temp = []
    for p in arr:
        temp.extend(p)

    q.append((0, x, y, temp))
    visited = set()

    while q:
        cnt, x, y, check_list = q.popleft()
        # visited.discard(tuple(check_list))
        if check_list == c:
            return cnt

        else:
            temp = [check_list[idx:idx + 3] for idx in range(0, 7, 3)]
            for i in range(4):
                nx, ny = x + dx[i], y + dy[i]
                if 0 <= nx < 3 and 0 <= ny < 3:

                    temp[x][y], temp[nx][ny] = swap(temp[x][y], temp[nx][ny])

                    concat_list = []
                    for i in temp:
                        concat_list.extend(i)

                    if tuple(concat_list) not in visited:
                        visited.add(tuple(concat_list))
                        q.append((cnt + 1, nx, ny, concat_list))
                    temp[x][y], temp[nx][ny] = swap(temp[x][y], temp[nx][ny])

    return -1


print(solve(x, y))
```
