---
author: ["Jxun-h"]
title: "[BOJ] 8911 거북이 with Python"
date: "2022-03-21"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "시뮬레이션", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/8911" target="_blank">BOJ 8911 거북이</a>

<br>

### 💡 조건

1.  2차원 평면 위에서 움직일 수 있는 거북이 로봇을 하나 가지고 있다. 거북이 로봇에게 내릴 수 있는 명령은 다음과 같이 네가지가 있다.  
    F: 한 눈금 앞으로  
    B: 한 눈금 뒤로  
    L: 왼쪽으로 90도 회전  
    R: 오른쪽으로 90도 회전
2.  L과 R명령을 내렸을 때, 로봇은 이동하지 않고, 방향만 바꾼다.  
    거북이는 항상 x축과 y축에 평행한 방향으로만 이동한다.
3.  거북이가 지나간 영역을 모두 포함할 수 있는 가장 작은 직사각형의 넓이를 구하는 문제.  
    단, 직사각형의 모든 변은 x축이나 y축에 평행이어야 한다.
4.  거북이는 가장 처음에 (0, 0)에 있고, 북쪽을 쳐다보고 있다.
5.  이 경우에 거북이가 지나간 영역을 모두 포함하는 직사각형은 선분이고, 선분은 한 변이 0인 직사각형으로 생각할 수 있다.  
    따라서, 선분의 경우에 넓이는 0이 된다.
6.  **구현, 시뮬레이션** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3
FFLF
FFRRFF
FFFBBBRFFFBBB
```

#### 실행결과

```py
2
0
9
```

<br>

### ⌨️ 문제 풀이

1.  문제에서 요구하는대로 구현을 하면 되는 문제입니다.
2.  방향값을 +1 해줄 때 4로 나눈 나머지를 구하면 더욱 편합니다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

for _ in range(int(stdin.readline())):
    x, y, direction = 0, 0, 0
    visited = set()
    for command in list(stdin.readline().rstrip()):
        if command == 'F':
            if direction == 0:
                y += 1

            elif direction == 1:
                x += 1

            elif direction == 2:
                y -= 1

            else:
                x -= 1

        elif command == 'B':
            if direction == 0:
                y -= 1

            elif direction == 1:
                x -= 1

            elif direction == 2:
                y += 1

            else:
                x += 1

        elif command == 'L':
            if direction == 0:
                direction = 3
            else:
                direction -= 1

        elif command == 'R':
            direction += 1
            direction %= 4

        visited.add((x, y))

    max_x, min_x = 0, 0
    max_y, min_y = 0, 0

    for x, y in visited:
        max_x, max_y = max(max_x, x), max(max_y, y)
        min_x, min_y = min(min_x, x), min(min_y, y)

    height = abs(max_y) + abs(min_y)
    width = abs(max_x) + abs(min_x)

    print(height * width)
```

<br>

### 💾 느낀점