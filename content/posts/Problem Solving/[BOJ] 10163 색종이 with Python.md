---
author: ["Jxun-h"]
title: "[BOJ] 10163 색종이 with Python"
date: "2022-03-09"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/10163" target="_blank">BOJ 10163 색종이</a>

<br>

### 💡 조건

1.  평면에 색깔이 서로 다른 직사각형 모양의 색종이 N장이 하나씩 차례로 놓여진다. 이때 색종이가 비스듬하게 놓이는 경우는 없다.
2.  색종이의 장수를 나타내는 정수 N (1 ≤ N ≤ 100)
3.  N장의 색종이가 주어진 위치에 차례로 놓일 경우, 각 색종이가 보이는 부분의 면적을 구하는 문제
4.  가로 최대 1001칸, 세로 최대 1001칸으로 구성된 격자 모양이다.  
    격자의 각 칸은 가로, 세로 길이가 1인 면적이 1인 정사각형
5.  색종이가 놓인 상태는 가장 왼쪽 아래 칸의 번호와 너비, 높이를 나타내는 네 정수로 표현한다.  
    예를 들어, 위 그림에서 회색으로 표시된 색종이는 (1,4)가 가장 왼쪽 아래에 있고 너비 3, 높이 2이므로 1 4 3 2로 표현한다.  
    색종이가 격자 경계 밖으로 나가는 경우는 없다.
6.  **구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4
0 2 10 10
7 9 8 4
8 4 10 6
6 0 12 10
```

#### 실행결과

```py
62
24
0
120
```

<br>

### ⌨️ 문제 풀이

1.  색종이의 정보를 입력받아서 가장 왼쪽 아래칸에서부터 놓는다.
2.  (1)번의 작업을 반복문을 통해서 board 에 채워넣는데, 이때 k의 값은 색종이의 번호를 뜻한다.
3.  색종이가 놓인 부분에서 가장 작은 좌표의 값과 가장 큰 좌표의 값을 계산하여 변수를 갱신한다.
4.  모든 입력을 받았다면, k를 순회하면서 각 색종이의 면적을 구해준다.
5.  각 번호에 알맞은 색종이의 면적은 res 변수에 k 번째에 더해지고, res를 순회하면서 출력하면 된다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
board = [[-1] * 1001 for _ in range(1001)]
res = [0 for _ in range(n)]
minx, miny = 1001, 1001
maxx, maxy = 0, 0

for k in range(n):
    x, y, width, height = map(int, stdin.readline().split())
    for i in range(x, x + width):
        for j in range(y, y + height):
            board[i][j] = k
    minx, miny = min(x, minx), min(y, miny)
    maxx, maxy = max(x + width, maxx), max(y + height, maxy)

for k in range(n):
    for i in range(minx, maxx):
        for j in range(miny, maxy):
            if board[i][j] == k:
                res[k] += 1

for i in res:
    print(i)
```

<br>

### 💾 느낀점

1.  pypy로 제출하여 풀었던 문제이다.
2.  서브태스크가 있는 문제라서 문제를 풀이할 때, 몇 번 틀리기도 했다.
3.  이 때, 구현이 참 힘들고 어려웠었는데, 성장했음을 느꼈다.