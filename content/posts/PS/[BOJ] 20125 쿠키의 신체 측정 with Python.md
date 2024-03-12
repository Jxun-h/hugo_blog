---
author: ["Jxun-h"]
title: "[BOJ] 20125 쿠키의 신체 측정 with Python"
date: "2022-05-12"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/20125" target="_blank">BOJ 20125 쿠키의 신체 측정</a>

<br>

### 💡 조건

1.  쿠키들은 신체를 측정하기 위해서 한 변의 길이가 N인 정사각형 판 위에 누워있으며, 어느 신체 부위도 판 밖으로 벗어나지 않는다.
2.  판의 x번째 행, y번째 열에 위치한 곳을 (x, y)로 지칭한다. 판의 맨 왼쪽 위 칸을 (1, 1), 오른쪽 아래 칸을 (N, N)으로 나타낼 수 있다.
3.  쿠키의 신체는 머리, 심장, 허리, 그리고 좌우 팔, 다리로 구성되어 있다.

    <center><img src='/20125.png' width="381" height="381"/></center>

4.  그림에서 빨간 곳으로 칠해진 부분이 심장이다. 머리는 심장 바로 윗 칸에 1칸 크기로 있다.  
    왼쪽 팔은 심장 바로 왼쪽에 붙어있고 왼쪽으로 뻗어 있으며, 오른쪽 팔은 심장 바로 오른쪽에 붙어있고 오른쪽으로 뻗어있다.  
    허리는 심장의 바로 아래 쪽에 붙어있고 아래 쪽으로 뻗어 있다.  
    왼쪽 다리는 허리의 왼쪽 아래에, 오른쪽 다리는 허리의 오른쪽 아래에 바로 붙어있고, 각 다리들은 전부 아래쪽으로 뻗어 있다.  
    각 신체 부위들은 절대로 끊겨있지 않으며 굽혀진 곳도 없다.  
    또한, 허리, 팔, 다리의 길이는 1 이상이며, 너비는 무조건 1이다.
5.  쿠키의 신체가 주어졌을 때 심장의 위치와 팔, 다리, 허리의 길이를 구하는 문제
6.  5 ≤ N ≤ 1,000. N은 판의 한 변의 길이를 의미하는 양의 정수다.
7.  ai,j는 * 또는 _이다. *는 쿠키의 신체 부분이고, _는 쿠키의 신체가 올라가 있지 않은 칸을 의미한다. (1 ≤ i, j ≤ N)
8.  쿠키의 신체 조건에 위배되는 입력은 주어지지 않는다.
9.  **구현** 유형의 문제

<br>

## 🔖 예제 및 실행결과

#### 예제

```py
5
_____
__*__
_***_
__*__
_*_*_
```

#### 실행결과

```py
3 3
1 1 1 1 1
```

<br>

### 🖥 소스 코드

```py
from sys import stdin

arr = []
n = int(stdin.readline())
for i in range(n):
    arr.append(list(stdin.readline().rstrip()))

heo, l_leg, r_leg = 0, 0, 0


def find_heart():
    for i in range(n):
        for j in range(n):
            if arr[i][j] == '*':
                return (i, j), (i + 1, j)


head, heart = find_heart()


l_arm = arr[heart[0]][:heart[1]].count('*')
r_arm = arr[heart[0]][heart[1] + 1:].count('*')

for i in range(heart[0] + 1, n):
    if arr[i][heart[1]] != '*':
        last_heo = (i, heart[1])
        break
    else:
        heo += 1

for i in range(last_heo[0], n):
    if arr[i][heart[1] - 1] == '*':
        l_leg += 1

    if arr[i][heart[1] + 1] == '*':
        r_leg += 1


print(heart[0] + 1, heart[1] + 1)
print(l_arm, r_arm, heo, l_leg, r_leg)
```
