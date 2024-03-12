---
author: ["Jxun-h"]
title: "[BOJ] 9372 상근이의 여행 with Python"
date: "2022-02-22"
description: ""
summary: ""
tags: ["자료구조", "PS", "그래프 이론", "유니온-파인드", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/9372" target="_blank">BOJ 9372 상근이의 여행</a>

<br>

### 💡 조건

1.  N개국을 여행할 상근이에게 가장 적은 비행기를 타고 여행할 수 있게 도와주자.
2.  테스트 케이스의 수 T(T ≤ 100)
3.  첫 번째 줄에는 국가의 수 N(2 ≤ N ≤ 1 000)과 비행기의 종류 M(1 ≤ M ≤ 10 000) 가 주어진다.  
    이후 M개의 줄에 a와 b 쌍들이 입력된다. a와 b를 왕복하는 비행기가 있다는 것을 의미한다. (1 ≤ a, b ≤ n; a ≠ b)  
    주어지는 비행 스케줄은 항상 연결 그래프를 이룬다.
4.  **그래프 이론, 유니온-파인드** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
2
3 3
1 2
2 3
1 3
5 4
2 1
2 3
4 3
4 5
```

#### 실행결과

```py
2
4
```

<br>

### ⌨️ 문제 풀이

1.  Union-Find 알고리즘을 사용하면 쉽게 풀 수 있습니다.
2.  parent 리스트에서 각 국은 본인의 번호를 가지고 있다.  
    만약 상근이가 a국가에서 b 국가를 간다고 입력을 받았으면, a와 b 국가의 parent 를 찾고, 만약 서로 같지 않다면 같은 부모에 속하도록 변경한다.
3.  (2)번 작업을 마친 뒤, res + 1
4.  res 를 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin


def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]


def union_parent(a, b, parent):
    a = find_parent(parent, a)
    b = find_parent(parent, b)

    if a < b:
        parent[a] = b
    else:
        parent[b] = a


for test_case in range(int(stdin.readline())):
    n, m = map(int, stdin.readline().split())
    nations = [x for x in range(n + 1)]
    res = 0
    for _ in range(m):
        a, b = map(int, stdin.readline().split())
        if find_parent(nations, a) != find_parent(nations, b):
            union_parent(a, b, nations)
            res += 1

    print(res)
```

<br>

### 💾 느낀점

1.  공항이라는 문제를 풀었던 기억이 있고, 유니온-파인드 알고리즘을 이용해 시도해 봤었던 기억이 있습니다.
2.  유파로 한번에 풀었던 문제입니다.