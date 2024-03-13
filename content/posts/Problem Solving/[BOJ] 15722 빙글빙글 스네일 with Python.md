---
author: ["Jxun-h"]
title: "[BOJ] 15722 빙글빙글 스네일 with Python"
date: "2022-02-27"
description: ""
summary: ""
tags: ["자료구조", "PS", "문자열", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/15722" target="_blank">BOJ 15722 빙글빙글 스네일</a>

<br>

### 💡 조건

1.  달팽이는 원점에서 시작하여 1초에 한 칸 씩, 시계방향으로 아래 그림과 같이 움직인다.
2.  1초일 때 달팽이의 위치는 (0, 1)이다.
3.  몇 초가 지났는지가 입력으로 주어질 때, 현재 달팽이의 위치를 좌표로 출력하는 문제
4.  달팽이가 움직인 시간이 n초로 주어진다. (0 ≤ n ≤ 1000, n은 0이상의 정수)
5.  **구현, 시뮬레이션** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```
9
```

#### 실행결과

```
-1 2
```

<br>

### ⌨️ 문제 풀이

1.  달팽이의 첫 위치를 [0, 0]으로 지정한다.
2.  cnt 가 n 과 같아질 때까지 반복을 할 것.
3.  i가 0일 때는 좌표 값을 더해주고, 1일 때는 좌표 값을 빼줄 것.
4.  좌표를 더해주거나 빼줄 때, cnt 를 1씩 증가시키고, i 를 순회할 때마다 length를 늘려준다  
    늘려준 length 는 좌표를 반복적으로 빼주고 더해줄 때 사용하는 변수
5.  mode 는 1 일 때 0으로, 0일 때 1로 변경해주는데, x, y 를 각각 더하고 빼줄 때 사용하는 것.
6.  함수가 반복적으로 좌표를 빼주고 더해주는 작업을 하다가, cnt가 n과 같아지면 좌표 pos 를 리턴한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin


def solve():
    n = int(stdin.readline())
    pos = [0, 0]
    mode, length = 0, 1
    cnt = 0
    while 1:
        for i in range(2):
            for _ in range(2):
                # Add
                if i == 0:
                    if mode == 0:
                        for _ in range(length):
                            pos[1] += 1
                            cnt += 1
                            if n == cnt:
                                return pos
                    else:
                        for _ in range(length):
                            pos[0] += 1
                            cnt += 1
                            if n == cnt:
                                return pos
                # Sub
                if i == 1:
                    if mode == 0:
                        for _ in range(length):
                            pos[1] -= 1
                            cnt += 1
                            if n == cnt:
                                return pos
                    else:
                        for _ in range(length):
                            pos[0] -= 1
                            cnt += 1
                            if n == cnt:
                                return pos

                mode = 1 if mode == 0 else 0

            length += 1


print(*solve())
```

<br>

### 💾 느낀점

1.  문제에서 설명해주는 대로 달팽이가 움직이는 방향을 잘 생각해서 구현해야 합니다.
2.  스스로 구현 실력이 부족하다고 생각했던 문제였습니다.