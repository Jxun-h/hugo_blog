---
author: ["Jxun-h"]
title: "[BOJ] 14562 태권왕 with Python"
date: "2022-05-12"
description: ""
summary: ""
tags: ["자료구조", "PS", "정렬", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/14562" target="_blank">BOJ 14562 태권왕</a>

<br>

### 💡 조건

1.  테스트 케이스의 수 C(1 ≤ C ≤ 100)  
    현재 점수 S와 T가 공백을 사이에 두고 주어진다. (1 ≤ S < T ≤ 100)
2.  태균이가 현재 할 수 있는 연속 발차기는 두가지가 있다.  
    A는 현재 점수만큼 점수를 얻을 수 있는 엄청난 연속 발차기이다. 하지만 상대 역시 3점을 득점하는 위험이 있다.  
    B는 1점을 얻는 연속 발차기이다.
3.  태균이의 점수 S와 상대의 점수 T가 주어질 때, S와 T가 같아지는 최소 연속 발차기 횟수를 구하는 문제
4.  **BFS(너비우선탐색)** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
6
10 20
2 7
15 62
10 37
11 50
34 59
```

#### 실행결과

```py
3
3
4
4
5
25
```

<br>

### ⌨️ 문제 풀이

1.  BFS로 점수를 얻을 수 있는 점수를 큐에 추가한다.
2.  (time + 1, s 16926 배열 돌리기 1* 2, t + 3)는 내가 현재 점수만큼 점수를 얻고, 상대방에게 점수를 3점 내어주는 상태.
3.  (time + 1, s + 1, t) 는 내가 1점만큼 점수를 얻을 수 있는 상태
4.  (현재 나의 점수 16926 배열 돌리기 1* 2)의 상태를 만든 적이 없다면 (2)번을,  
    (현재나의 점수 + 1)의 상태를 만든적이 없다면 (3)번의 상태를 큐에 넣어준다.
5.  현재 나의 점수와 상대방의 점수가 같으면 return

<br>

### 🖥 소스 코드

```py
from sys import stdin
from collections import deque


def solve(s, t):
    q = deque()
    q.append((0, s, t))

    while q:
        time, s, t = q.popleft()

        if s == t:
            return time

        if (t + 3) >= s * 2:
            if use[s * 2] == -1:
                q.append((time + 1, s * 2, t + 3))

        if use[s + 1] == -1:
            q.append((time + 1, s + 1, t))


for _ in range(int(stdin.readline())):
    s, t = map(int, stdin.readline().split())
    use = [-1 for _ in range(100001)]
    print(solve(s, t))
```
