---
author: ["Jxun-h"]
title: "[BOJ] 2637 장난감 조립 with Python"
date: "2022-06-01"
description: ""
summary: ""
tags: ["자료구조", "PS", "위상정렬", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2637" target="_blank">BOJ 2637 장난감 조립</a>

<br>

### 💡 조건

1.  우리는 어떤 장난감을 여러 가지 부품으로 조립하여 만들려고 한다.  
    이 장난감을 만드는데는 기본 부품과 그 기본 부품으로 조립하여 만든 중간 부품이 사용된다.

2.  기본 부품은 다른 부품을 사용하여 조립될 수 없는 부품이다. 중간 부품은 또 다른 중간 부품이나 기본 부품을 이용하여 만들어지는 부품이다.

3.  어떤 장난감 완제품과 그에 필요한 부품들 사이의 관계가 주어져 있을 때 하나의 장난감 완제품을 조립하기 위해  
    필요한 기본 부품의 종류별 개수를 계산하는 문제.

4.  자연수 N(3 ≤ N ≤ 100), 1부터 N-1까지는 기본 부품이나 중간 부품의 번호를 나타내고, N은 완제품의 번호를 나타낸다.

5.  자연수 M(3 ≤ M ≤ 100)이 주어지고, 그 다음 M개의 줄에는 어떤 부품을 완성하는데 필요한 부품들 간의 관계가 3개의 자연수 X, Y, K로 주어진다.  
    "중간 부품이나 완제품 X를 만드는데 중간 부품 혹은 기본 부품 Y가 K개 필요하다"는 뜻

6.  하나의 완제품을 조립하는데 필요한 기본 부품의 수를 한 줄에 하나씩 출력하되(중간 부품은 출력하지 않음)  
    반드시 기본 부품의 번호가 작은 것부터 큰 순서가 되도록 한다. 각 줄에는 기본 부품의 번호와 소요 개수를 출력한다.  
    정답은 2,147,483,647 이하이다.

7.  **위상 정렬 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
7
8
5 1 2
5 2 2
7 5 2
6 5 2
6 3 3
6 4 4
7 6 3
7 4 5
```

#### 실행결과

```py
1 16
2 16
3 9
4 17
```

<br>

### ⌨️ 문제 풀이

1.  문제에서 가장 중요한 문장을 먼저 살펴보겠다.

    `장난감을 만드는데는 기본 부품과 그 기본 부품으로 조립하여 만든 중간 부품이 사용된다.`

    `기본 부품은 다른 부품을 사용하여 조립될 수 없는 부품이다.` 

    `중간 부품은 또 다른 중간 부품이나 기본 부품을 이용하여 만들어지는 부품이다.`
3.  요약하자면, 중간 부품과 기본 부품을 필요 개수 이상 만들어두어야 완제품을 만들 수 있으며,  
    중간 부품은 기본 부품을 조립하여 만들 수 있다. 이는 반드시 기본 부품을 으로 중간 제품을 먼저 만들어야 완제품을  
    만들 수 있다는 것 이다.

3.  위상 정렬은 순서가 있는 작업을 차례대로 수행해야할 때 그 순서를 결정해주기 위해 사용하는 알고리즘이다.  
    각 중간 부품이 만들어지기 위해서는 몇 개의 기본 부품이 반드시 있어야하기 때문에 위상정렬을 통해 문제를 해결할 수 있다는 생각을 할 수 있다.

4.  필요한 개수를 needs 리스트에 저장하고, needs[n] 에서 각 부품의 개수를 번호 순서대로 출력할 것이다.

5.  connect 리스트에는 X 를 만들기 위한 Y번 부품 K 개에 대해 저장한다.

<br>

### 🖥 소스 코드

```py
import sys
from collections import deque

input = sys.stdin.readline
n = int(input())

connect = [[] for _ in range(n + 1)]
needs = [[0] * (n + 1) for _ in range(n + 1)]

q = deque()
degree = [0] * (n + 1)

for _ in range(int(input())):
    a, b, c = map(int, input().split())
    connect[b].append((a, c))
    degree[a] += 1

for i in range(1, n + 1):
    if degree[i] == 0:
        q.append(i)

while q:
    now = q.popleft()

    for next, next_need in connect[now]:
        if needs[now].count(0) == n + 1:
            needs[next][now] += next_need
        else:
            for i in range(1, n + 1):
                needs[next][i] += needs[now][i] * next_need

        degree[next] -= 1
        if degree[next] == 0:
            q.append(next)

for x in enumerate(needs[n]):
    if x[1] > 0:
        print(*x)
```

<br>

### 💾 느낀점

1.  위상 정렬의 개념 정리를 통해 문제의 컨셉을 이해함.

2.  순서가 있는 작업을 차례대로 수행하거나, 반드시 전제 조건이 만족되어야할 때를 잘 파악하여 생각하고  
    그 로직을 구현하는 연습을 할 수 있었던 문제였다. 하지만 난이도는 상당한 것 같다.

3.  자꾸 까먹는 위상 정렬같은 문제는 코딩테스트 후반 번호로 등장할 가능성이 있을 것 같다.