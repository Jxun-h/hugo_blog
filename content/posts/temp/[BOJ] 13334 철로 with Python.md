---
author: ["Jxun-h"]
title: "[BOJ] 13334 철로 with Python"
date: "2021-10-25"
description: ""
summary: ""
tags: ["자료구조", "PS", "우선순위큐", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/13334" target="_blank">BOJ 13334 철로</a>

<br>

### 💡 조건

1.  사람 수를 나타내는 양의 정수 `n` `(1 ≤ n ≤ 100,000)`  
    `n`개의 각 줄에 정수 쌍 `(hi, oi)`가 주어진다.  
    `−100,000,000 ≤ hi ≤ 100,000,000`  
    `−100,000,000 ≤ oi ≤ 100,000,000`  
    `oi != hi`  
    철로의 길이를 나타내는 정수 `d` `(1 ≤ d ≤ 200,000,000)`
2.  집과 사무실 모두가 철로 길이 안에 들어갈 수 있는 최대의 개수를 구하는 문제.
3.  **우선순위 큐, 즉 자료구조를 활용하는 문제.**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
8
5 40
35 25
10 20
10 25
30 50
50 60
30 25
80 100
30
```

#### 실행결과

```python
4
```

### ⌨️ 문제 풀이

1.  가장 먼저 집과 사무실의 위치를 입력받는데, 그 위치가 정렬이 된 데이터가 아니기에 계산을 용이하도록 하기 위해  
    데이터를 전처리를 해준 후, `data` 리스트에 넣는다.

2.  철로의 길이를 입력받는다.

3.  `data`를 순회하면서, 집과 사무실의 거리가 철로의 길이보다 짧을 경우에만 `roads` 리스트에 넣어준다.  
    **모든 곳에서의 선분 d(철로의 길이) 안에 집과 사무실이 모두 안에 들어가야 하기 때문이다.**

4.  3번을 수행시켜 얻은 `roads` 리스트를 정렬시킨다.

5.  정렬시킨 `roads` 배열을 다시 순회하면서, `heapq` 를 만들어 큐가 비어있을 경우 정렬된 데이터를 넣는다.

6.  `큐`의 시작점 위치가 `(현재 지정된 road의 끝나는 지점 - 철로 길이)` 보다 짧으면 `큐`에서 데이터를 뺀다.  
    `큐`에 들어가 있는 집과 사무실 좌표 `순서쌍의 개수`가 정답이기 때문에  
    철로의 길이 범위 밖으로 좌표가 나가는 애들은 과함하게 잘라준다.

<br>

### 🖥 소스 코드

```python
from sys import stdin
import heapq

n = int(stdin.readline())
roads, data = [], []

for _ in range(n):
    data.append(sorted(list(map(int, stdin.readline().split()))))
train_road_length = int(stdin.readline())


for road in data:
    s, e = road
    if (e - s) <= train_road_length:
        roads.append(road)

roads.sort(key=lambda x: x[1])

answer = 0
q = []

for road in roads:
    if not q:
        heapq.heappush(q, road)
    else:
        while q[0][0] < road[1] - train_road_length:
            heapq.heappop(q)
            if not q:
                break

        heapq.heappush(q, road)
    answer = max(answer, len(q))

print(answer)
```

<br>

### 💾 느낀점

1.  `우선순위 큐`를 사용해서 푸는 문제였지만, 문제를 이해하고 푸는데에 애를 먹었다.
2.  `누적합`을 사용해서 풀어보려고 했는데 올바른 풀이가 아니었는지, 코딩을 하다가 몇 번 뒤집었다.
3.  이 문제 또한 반드시 한번 더 풀어보고 개념을 익혀야할 문제인 것 같다.