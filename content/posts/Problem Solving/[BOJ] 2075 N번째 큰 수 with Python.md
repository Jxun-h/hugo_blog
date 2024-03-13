---
author: ["Jxun-h"]
title: "[BOJ] 2075 N번째 큰 수 with Python"
date: "2022-02-21"
description: ""
summary: ""
tags: ["자료구조", "PS", "우선순위 큐", "정렬", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2075" target="_blank">BOJ 2075 N번째 큰 수</a>

<br>

### 💡 조건

1.  N×N의 표에 수 N2개 채워져 있다. 채워진 수에는 한 가지 특징이 있는데,  
    **모든 수는 자신의 한 칸 위에 있는 수보다 크다는 것**이다.
2.  표에 채워진 수는 모두 다르다.
3.  N(1 ≤ N ≤ 1,500)
4.  표에 적힌 수는 -10억보다 크거나 같고, 10억보다 작거나 같은 정수이다.
5.  **자료구조 응용, 우선순위 큐 활용, 정렬** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5
12 7 9 15 5
13 8 11 19 6
21 10 26 31 16
48 14 28 35 25
52 20 32 41 49
```

#### 실행결과

```py
35
```

<br>

### ⌨️ 문제 풀이

1.  q 라는 리스트를 만든다. 이 리스트는 표의 셀마다의 숫자를 넣을 것이며, 우선순위 큐로 사용된다.
2.  각 숫자를 cnt 변수가 입력 받은 n과 같을 때까지 cnt + 1을 해주며 q 에 넣는다.
3.  만약 q[0]의 값보다 방금 순회하고 있는 값이 크다면  
    우선순위가 가장 높은 것을 꺼내고, 순회하고 있는 값을 넣는다.
4.  모든 데이터를 순회했다면, q 를 정렬하고 가장 첫번째에 있는 값을 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
import heapq

n = int(stdin.readline())
q = []
cnt = 0
for _ in range(n):
    data = list(map(int, stdin.readline().split()))
    for j in data:
        if cnt != n:
            heapq.heappush(q, j)
            cnt += 1
        else:
            if q[0] < j:
                heapq.heappop(q)
                heapq.heappush(q, j)

q.sort()
print(q[0])
```

<br>

### 💾 느낀점

1.  우선순위 큐의 성질을 이용하는 문제였습니다.
2.  자료구조의 강의를 듣기 전, 우선순위큐는 대충 이런 느낌이지~ 라는 생각으로 풀었는데  
    자료구조 강의를 보고 문제를 다시 보니 이런 꿀 골드문제가 없습니다.