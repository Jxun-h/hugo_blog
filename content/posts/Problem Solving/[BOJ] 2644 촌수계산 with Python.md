---
author: ["Jxun-h"]
title: "[BOJ] 2644 촌수계산 with Python"
date: "2022-06-13"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2644" target="_blank">BOJ 2644 촌수계산</a>

<br>

### 💡 조건

1.  기본적으로 부모와 자식 사이를 1촌으로 정의하고 이로부터 사람들 간의 촌수를 계산한다.

2.  아버지와 할아버지는 각각 1촌으로 나와 할아버지는 2촌이 되고, 아버지 형제들과 할아버지는 1촌, 나와 아버지 형제들과는 3촌이 된다.

3.  여러 사람들에 대한 부모 자식들 간의 관계가 주어졌을 때, 주어진 두 사람의 촌수를 계산하는 프로그램을 작성하시오.

4.  사람들은 1, 2, 3, …, n (1 ≤ n ≤ 100)의 연속된 번호로 각각 표시된다.  
    입력 파일의 첫째 줄에는 전체 사람의 수 n이 주어지고, 둘째 줄에는 촌수를 계산해야 하는 서로 다른 두 사람의 번호가 주어진다.

5.  셋째 줄에는 부모 자식들 간의 관계의 개수 m이 주어진다.  
    넷째 줄부터는 부모 자식간의 관계를 나타내는 두 번호 x,y가 각 줄에 나온다. 이때 앞에 나오는 번호 x는 뒤에 나오는 정수 y의 부모 번호를 나타낸다.

7.  각 사람의 부모는 최대 한 명만 주어진다.  
    입력에서 요구한 두 사람의 촌수를 나타내는 정수를 출력한다.  
    어떤 경우에는 두 사람의 친척 관계가 전혀 없어 촌수를 계산할 수 없을 때가 있다. 이때에는 -1을 출력해야 한다.

6.  **BFS, 그래프탐색** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
9
8 6
7
1 2
1 3
2 7
2 8
2 9
4 5
4 6
```

#### 실행결과

```py
-1
```

<br>

### ⌨️ 문제 풀이

1.  촌수를 계산하여 몇 촌인지 출력하려고 하는 문제이기 때문에 그래프 탐색으로 풀이할 수 있다.

2.  요구한 두 사람의 촌수를 구해야하기 때문에 양방향 그래프를 만들어 BFS를 사용해 촌수를 구하고 출력하면 된다.

3.  BFS 알고리즘을 통해 나온 값이 False 라면 -1을 출력하고 아니라면 결과값을 출력하면 된다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from collections import deque

n = int(stdin.readline())
a, b = map(int, stdin.readline().split())

graph = [[] for _ in range(n + 1)]
for _ in range(int(stdin.readline())):
    k, p = map(int, stdin.readline().split())
    graph[k].append(p)
    graph[p].append(k)


def solve(x):
    q = deque()
    q.append((x, 0))
    visited = set()
    visited.add(x)

    while q:
        now, c = q.popleft()

        if now == b:
            return c

        for i in graph[now]:
            if i not in visited:
                q.append((i, c + 1))
                visited.add(i)

    return False


ans = solve(a)
print(ans) if ans else print(-1)
```
