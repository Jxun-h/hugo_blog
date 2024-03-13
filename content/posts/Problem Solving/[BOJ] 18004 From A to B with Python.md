---
author: ["Jxun-h"]
title: "[BOJ] 18004 From A to B with Python"
date: "2022-05-15"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "그리디", "BFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/18004" target="_blank">BOJ 18004 From A to B</a>

<br>

### 💡 조건

1.  두 개의 정수인 a와 b가 입력된다.
2.  일련의 작업을 수행하여 a를 b로 만들려고 한다.
3.  다음의 두가지 작업만 할 수 있다.
    1.  짝수인 경우에만 2로 나누기.
    2.  1 더하기
4.  (1 ≤ a , b ≤ 10 9 )
5.  a 를 b 로 변환하는 데 필요한 주어진 연산의 최소 횟수를 출력하는 문제
6.  **수학, 그리디 알고리즘, BFS** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
103 27
```

#### 실행결과

```py
4
```

<br>

### ⌨️ 문제 풀이

1.  a 와 b 정수를 입력받고, a 를 b로 만드는 문제이다.
2.  a에 연산할 수 있는 두가지 연산을 가지고 b를 만들어야하는데, 나누기와 더하기 1이다.
3.  문제의 첫번째 연산은 a를 작게 만드는 연산인만큼, a가 b보다 작으면 할 필요가 없는 연산이다.
4.  BFS 알고리즘을 통해서 queue에 a를 연산한 값과 연산한 횟수를 넣어 관리한다.
5.  (3)번 조건에 의해 queue에서 뽑아낸 연산된 a가 b보다 작아지면 현재 연산한 횟수와 (b - queue에서 뽑아낸 연산된 a)값을 더해 리턴한다.

<br>

### 🖥 소스 코드

```py
from collections import deque
from sys import stdin

a, b = map(int, stdin.readline().split())


def solve():
    q = deque()
    if a <= b:
        print(b - a)
        return

    q.append((0, a))
    while q:
        cost, now = q.popleft()

        if now == b:
            print(cost)
            return

        if now > b:
            if now % 2 == 0:
                q.append((cost + 1, now // 2))
            else:
                q.append((cost + 1, now + 1))
        else:
            print(cost + (b - now))
            return


solve()
```
