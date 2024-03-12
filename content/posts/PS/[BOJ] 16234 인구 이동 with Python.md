---
author: ["Jxun-h"]
title: "[BOJ] 16234 인구 이동 with Python"
date: "2022-02-03"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "BFS", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/16234" target="_blank">BOJ 16234 인구 이동</a>

<br>

### 💡 조건

1.  N×N크기의 땅이 있고, 땅은 1×1개의 칸으로 나누어져 있다.  
    N, L, R이 주어진다. (1 ≤ N ≤ 50, 1 ≤ L ≤ R ≤ 100)
2.  인구 이동은 하루 동안 다음과 같이 진행되고, 더 이상 아래 방법에 의해 인구 이동이 없을 때까지 지속된다.
    -   1.  국경선을 공유하는 두 나라의 인구 차이가 L명 이상, R명 이하라면, 두 나라가 공유하는 국경선을 오늘 하루 동안 연다.
    -   2.  위의 조건에 의해 열어야하는 국경선이 모두 열렸다면, 인구 이동을 시작한다.
    -   3.  국경선이 열려있어 인접한 칸만을 이용해 이동할 수 있으면, 그 나라를 오늘 하루 동안은 연합이라고 한다.
    -   4.  연합을 이루고 있는 각 칸의 인구수는 (연합의 인구수) / (연합을 이루고 있는 칸의 개수)가 된다.
    -   5.  연합을 해체하고, 모든 국경선을 닫는다.
3.  각 나라의 인구수가 주어졌을 때, 인구 이동이 며칠 동안 발생하는지 구하는 프로그램을 작성해야한다.
4.  r행 c열에 주어지는 정수는 A\[r\]\[c\]의 값이다. (0 ≤ A\[r\]\[c\] ≤ 100)
5.  **BFS 알고리즘, 구현**유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
2 20 50
50 30
30 40
```

#### 실행결과

```py
1
```

<br>

### ⌨️ 문제 풀이

1.  board 리스트에 각 국가의 인구수를 입력 받고, 인구 이동 횟수를 저장할 cnt 변수를 0으로 초기화.
2.  인구 이동이 일어나지 않을 때까지 while 반복을 통해서 체크를 해줄 것.
3.  인구 이동이 일어났을 때, 인구 이동 후의 인구 수와 인구 이동이 일어난 도시의 좌표를 담을 리스트 변수 tf를 생성한다.
4.  board 를 순회하면서, 각 좌표에서 연합이 될 수 있는 국가를 체크하여 반환된 값을 temp에 저장한다.  
    만약, temp 가 False라면 인구이동이 일어나지 않은 것이다.  
    반대로 False 가 아니라면 인구이동이 일어난 것이다.
5.  board 전체를 순회했음에도 인구이동이 일어나지 않아 tf가 비어있다면, 그대로 while 문 밖으로 나온다.
6.  tf가 비어있지 않다면, 인구이동 횟수(cnt)를 + 1 해준 뒤,  
    tf 를 순차적으로 순회하면서, 연합끼리의 인구 이동을 한 좌표에 해당하는 인구 수로 board 값을 갱신한다.
7.  check() 함수의 로직은 아래와 같다.
    1.  BFS 알고리즘을 이용하여 매개변수로 받은 좌표와 연합이 될 수 있는 모든 국가를 찾는다.
    2.  다음 이동하려는 좌표가 방문하지 않았어야하고,  
        그 좌표에 해당하는 board의 값이 l <= 국경을 공유하는 국가들의 인구 차이 <= r 의 조건을 지켜야한다.
    3.  또한 (1), (2) 의 조건을 지킨 경우, 연합들의 각 인구수는 vals 리스트에 저장해 평균 인구수를 계산할 수 있게 한다.
    4.  check 함수 내의 인구이동 판별 변수인 tf 에 인구이동을 했을 시, True 값을 저장한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from collections import deque

n, l, r = map(int, stdin.readline().split())
if l > r:
    l, r = r, l

board = []
for _ in range(n):
    board.append(list(map(int, stdin.readline().split())))

dx, dy = [1, 0, 0, -1], [0, -1, 1, 0]


def check(x, y):
    visited = set()
    q = deque()
    visited.add((x, y))
    q.append((x, y, board[x][y]))
    vals = [board[x][y]]
    tf = False

    while q:
        x, y, cost = q.popleft()

        for i in range(4):
            nx, ny = x + dx[i], y + dy[i]
            if -1 < nx < n and -1 < ny < n:
                if l <= abs(cost - board[nx][ny]) <= r and (nx, ny) not in visited:
                    visited.add((nx, ny))
                    q.append((nx, ny, board[nx][ny]))
                    vals.append(board[nx][ny])
                    tf = True

    if not tf:
        return False
    else:
        res = int(sum(vals) / len(vals))
        return [res, visited]


cnt = 0
while 1:
    tf = []
    for i in range(n):
        for j in range(n):
            temp = check(i, j)
            if temp is not False:
                tf.append(temp)

    if not tf:
        break
    else:
        cnt += 1
        for val, visited in tf:
            for x, y in visited:
                board[x][y] = val

print(cnt)
```

<br>

### 💾 느낀점

1.  국경선을 공유하는 두 국가의 인구 차이 조건을 넣는 것에서 한번 헤맸다.
2.  연합으로 구성된 국가들의 인구 평균 수를 구하는 방법에서 고민을 했었다.
3.  모든 연합을 따로 구해서 연합끼리의 평균 인구 수로 갱신하는 부분이 한번에 이루어져야 한다.
4.  하지만 (3)의 방식이 아닌 연합이 생길때마다 변경해주어 예제 결과도 다르게 나오는 대참사가 있었다.
5.  BFS 알고리즘 중에서도 조건이 꽤 있어서 구현이 조금 묻어나온 문제 같았고, 풀기 조금 힘이 들었다.