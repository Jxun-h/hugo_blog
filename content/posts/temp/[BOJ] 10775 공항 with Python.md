---
author: ["Jxun-h"]
title: "[BOJ] 10775 공항 with Python"
date: "2021-10-13"
description: ""
summary: ""
tags: ["유니온-파인드", "PS", "Union-find", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/10775" target="_blank">BOJ 10775 공항</a>

<br>

## 💡 조건 및 풀이

1.  공항에는 `G개의 게이트`가 있으며 각각은 `1에서 G까지의 번호`를 가지고 있다.
2.  공항에는 P개의 비행기가 순서대로 도착할 예정.
3.  `i번째 비행기`를 1번부터 `gi (1 ≤ gi ≤ G)` 번째 게이트중 하나에 영구적으로 도킹
4.  비행기가 어느 게이트에도 도킹할 수 없다면 공항이 폐쇄되고, 이후 어떤 비행기도 도착할 수 없다.
5.  **Union - Find 알고리즘 유형의 문제**
6.  비행기를 최대 몇 대 도킹시킬 수 있는지 구하는 문제.
7.  `게이트의 수 G (1 ≤ G ≤ 105)`  
    `비행기의 수 P (1 ≤ P ≤ 105)`  
    `P개의 줄에 gi (1 ≤ gi ≤ G)`

<br>

## 🔖 예제 및 실행결과

#### 예제

```python
4
3
4
1
1
```

#### 실행결과

```python
2
```

<br>

## ⌨️ 문제 풀이

1.  각 비행기의 번호를 입력 받을 때 1부터 시작하기 때문에 게이트 수 + 1 만큼 배열 parent 를 생성한다.
2.  배열의 원소값은 각 인덱스 값과 동일하게 하는데, 이것을 부모를 자신으로 둔 것이라고 생각하면 좋다.
3.  비행기의 번호 gi 를 입력 받아 gi의 부모를 찾는다.
4.  `data = find_parent(parent, gi)`
5.  만약 data 가 존재하지 않는 0번 게이트에 도킹을 해야할 경우 반복문을 중단한다.
6.  4번 이 아니라면 res += 1.
7.  gi 번 비행기가 data 번 게이트에 도킹을 했고, 그 게이트에는 다른 비행기가 도킹 할 수 없으니  
    data - 1 번호의 게이트를 가리키는 게이트가 됐다고 생각하자.
8.  `union_parent(parent, data, data - 1)`
9.  순서대로 들어오는 비행기를 반복적으로 수행하다, 4번 의 조건에 걸리는 경우 반복문을 중단하고 결과를 출력한다.

<br>

## 🖥 소스 코드

```python
from sys import stdin


def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]


def union_parent(parent, a, b):
    a = find_parent(parent,a)
    b = find_parent(parent,b)

    if a >b:
        parent[a] = b
    else:
        parent[b] = a


g = int(stdin.readline())
p = int(stdin.readline())

parent = [x for x in range(g + 1)]
res = 0

for i in range(p):
    gi = int(stdin.readline())

    data = find_parent(parent, gi)
    if data == 0:
        break
    res += 1
    union_parent(parent, data, data - 1)

print(res)
```

<br>

## 💾 느낀점

-   내가 좋아하는 Union-Find 문제이다.
-   처음 풀어보는 유형이라 조금 헷갈리긴 했지만, 게이트와 비행기의 관계를 조금 파악하니  
    소스코드라도 짜면서 시도해볼 수 있었다.
-   유파 알고리즘 문제는 find\_parent, union\_parent 의 로직을 외워두니 훨~씬 수월했다.