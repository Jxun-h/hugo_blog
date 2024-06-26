---
author: ["Jxun-h"]
title: "[BOJ] 13305 주유소 with Python"
date: "2021-09-22"
description: ""
summary: ""
tags: ["구현", "PS", "그리디", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/13305" target="_blank">BOJ 13305 주유소</a>

<br>

### 💡 조건 및 풀이

1.  도시의 개수 `2 <= N <= 100000`
2.  도시를 연결하는 간선의 길이가 `N-1`개 주어진다.
3.  **그리디 알고리즘 유형 문제**
4.  제일 왼쪽에서 오른쪽으로 이동하는 최소 비용을 계산
5.  **어느 도시에서 기름을 넣어 이동하는 것이 가장 비용이 저렴한지에 대해 계산**하면 된다.
6.  **서브태스크 점수**가 주어진다
    1. 17점 모든 주유소의 리터당 가격은 1원
    2. 41점 `2 <= N <= 1000`  
           제일 왼쪽 도시부터 제일 오른쪽 도시까지의 거리는 최대 10000,  
           리터 당 가격은 최대 10000
    3. 42점 원래의 제약조건 이외에 아무 제약조건이 없다.

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
4
2 3 1
5 2 4 1
```

#### 실행결과

```python
18
```

<br>

### ⌨️ 문제 풀이

1.  도로의 길이를 저장할 리스트 `dist`  
    주유소의 리터당 가격을 저장할 리스트 `cost`
2.  가장 왼쪽에 있는 도시의 주유소의 리터당 가격을 변수 `c` 에 넣어준다.
3.  `k-1` 반복문을 실행하여 주유소의 리터 당 가격을 순회한다.
4.  **만약 현재 계산된 `c` 가 `i` 번째 리터 당 가격보다 비싸다면 `c` 를 갱신한다.**  
    **그게 아니라면, 결과값을 저장할 `res`에 `리터 당 가격 * i번째 도로의 길이`를 더해준다**

<br>

### 🖥 소스 코드

```python
from sys import stdin

k = int(stdin.readline())
dist = list(map(int, stdin.readline().split()))
cost = list(map(int, stdin.readline().split()))
res = 0

c = cost[0]
for i in range(k - 1):
    if c > cost[i]:
        c = cost[i]
    res += c * dist[i]

print(res)
```

<br>

### 💾 느낀점

- 그리디 문제라고해서 얕봤다가 로직이 한순간 꼬여서 고생을 좀 했다.
- 리스트를 따로 처리해 사용하다가 머리가 순간 복잡해지는 것을 방지하기 위해 노력을 해야겠다.
- 그림을 그려 차분히 로직을 생각하고 구현하는 습관을 길러야겠다.
