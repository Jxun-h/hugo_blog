---
author: ["Jxun-h"]
title: "[BOJ] 17204 죽음의 게임 with Python"
date: "2022-05-19"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/17204" target="_blank">BOJ 17204 죽음의 게임</a>

<br>

### 💡 조건

1.  게임에 참여하는 N명의 사람들은 원탁에 둘러앉게 된다.  
    N(3 ≤ N ≤ 150)

2.  게임을 시작하는 사람은 0번, 그 오른쪽 사람은 1번, 그 오른쪽은 2번, N-1번의 오른쪽 사람은 다시 0번이 된다.

3.  게임 참여자들간에 지목을 완료한 상태가 주어질때, 보성이가 벌주를 마시기 위해 록 하자.  
    영기가 불러야 하는 가장 작은 양의 정수 M을 보성이 몰래 귀띔해 주도록 하자.  
    보성이의 번호 K(1 ≤ K ≤ N - 1)

4.  김영기는 게임을 제안하였기에 자연스럽게 0번이 된다.

5.  N줄에 걸쳐 i(0 ≤ i ≤ N - 1)번 사람이 지목하는 사람의 번호 ai(0 ≤ ai ≤ N - 1)가 주어진다.  
    자기 자신을 지목하는 경우도 존재할 수 있다.  
    영기가 말해야 하는 가장 작은 양의 정수 M을 출력한다. 만약 어떤 방법으로도 보성이가 걸리지 않는다면 -1을 출력한다.

6.  **BFS, 그래프탐색** 유형의 문제

<br>

## 🔖 예제 및 실행결과

#### 예제

```py
5 3
1
3
2
1
4
```

#### 실행결과

```py
2
```

<br>

## ⌨️ 문제 풀이

1.  N줄에 걸쳐 i번 사람이 지목하는 사람의 번호를 입력받아 그래프를 만들어준다.

2.  BFS 알고리즘을 통해 순회할 것인데 게임을 제한하고 시작한 사람은 0번이기 때문에 0번부터 시작을 해서 K번이 지목되는 숫자를 세어 주면 된다.

3.  Queue 에는 몇번째로 지목되었는지, 지목된 사람이 누구인지에 대한 데이터를 넣어준다.

4.  BFS를 위해 만들어 둔 Queue에서 원소를 뽑았을 때, K번이라면 number를 리턴해준다.

5.  만약 BFS 로 그래프를 순회하면서 K를 지목할 수 없다면 -1을 return 해준다.

<br>

### 🖥 소스 코드

```py
from collections import deque
from sys import stdin

n, m = map(int, stdin.readline().split())
arr = [[] for _ in range(n + 1)]

for i in range(n):
    arr[i].append(int(stdin.readline()))


def solve(x):
    q = deque()
    q.append((0, x))
    visited = set()

    while q:
        number, x = q.popleft()

        if number > n and m not in visited:
            return -1

        if x == m:
            return number

        if arr[x][0]:
            q.append((number + 1, arr[x][0]))

    return -1


print(solve(0))
```
