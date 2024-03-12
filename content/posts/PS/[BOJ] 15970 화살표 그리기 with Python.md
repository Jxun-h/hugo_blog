---
author: ["Jxun-h"]
title: "[BOJ] 15970 화살표 그리기 with Python"
date: "2022-02-20"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/15970" target="_blank">BOJ 15970 화살표 그리기</a>

<br>

### 💡 조건

1.  부분 점수가 있는 문제.
2.  점들의 개수를 나타내는 정수 N
3.  N개의 줄 각각에는 점의 좌표와 색깔을 나타내는 두 정수 x와 y가 주어진다.
4.  모든 점에서 시작하는 화살표들의 길이 합을 출력하는 문제.
5.  각 점은 N개의 색깔 중 하나를 가진다.
6.  각 점 p에 대해서, p에서 시작하는 직선 화살표를 이용해서 다른 점 q에 연결하려고 한다.  
    여기서, 점 q는 p와 같은 색깔의 점들 중 p와 거리가 가장 가까운 점이어야 한다.  
    만약 가장 가까운 점이 두 개 이상이면 아무거나 하나를 선택한다.
7.  **브루트포스**유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5
0 1
1 2
3 1
4 2
5 1
```

#### 실행결과

```py
13
```

<br>

### ⌨️ 문제 풀이

1.  n을 입력 받은 뒤, n개의 점의 위치화 색의 번호를 입력 받는다.
2.  입력 받은 각 점의 위치와 색의 번호는 arr 리스트에 저장한다.
3.  arr 리스트를 순회한다.  
    점의 색깔이 0이 아닌 경우, solve(색, 위치) 에 넘겨준다.
4.  solve 함수 내부에서 다시 arr 리스트를 순회하면서, 점의 위치는 같지 않으나 색깔이 같은 점을 찾는다.
5.  같은 색깔의 점이 있다면 가장 작은 점의 거리를 min_cost 에 저장하고 반환한다.
6.  반환값을 res 에 더해 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
arr = []

for _ in range(n):
    x, y = map(int, stdin.readline().split())
    arr.append((x, y))


def solve(color, idx):
    min_cost = int(1e9)
    for t_idx, t_color in arr:
        if t_idx != idx and t_color == color:
            if abs(idx - t_idx) < min_cost:
                min_cost = abs(idx - t_idx)

    return min_cost


res = 0
for idx, color in arr:
    if color != 0:
        res += solve(color, idx)
print(res)
```

<br>

### 💾 느낀점

1.  자칫 잘못생각하면 어렵게 느껴질 문제였던 것 같습니다.
2.  입력받은 n의 크기를 보고 시간초과가 나지 않을 것이라고 판단하고 풀이해서 쉽게 풀었습니다.