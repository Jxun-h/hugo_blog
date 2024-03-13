---
author: ["Jxun-h"]
title: "[BOJ] 17839 Baba is Rabbit with Python"
date: "2022-05-13"
description: ""
summary: ""
tags: ["자료구조", "PS", "그래프 탐색", "BFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/17839" target="_blank">BOJ 17839 Baba is Rabbit</a>

<br>

### 💡 조건

1.  N(1 ≤ N ≤ 100,000)
2.  N개의 줄에 걸쳐 명령이 주어진다.  
    각 명령은 p is q의 형태로 주어지며, p와 q는 첫 글자가 영문 대문자이고, 나머지 글자는 영문 소문자인 길이 10 이내의 문자열이다.
3.  Baba에 명령을 한 번 이상 적용한 결과로 나올 수 있는 사물을 사전순으로 출력한다.  
    단, 적용할 수 있는 명령이 없다면, 아무것도 출력하지 않는다.
4.  **그래프 탐색, BFS** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
1
Rabbit is Carrot
```

#### 실행결과 1
```py

```

#### 예제 2

```py
3
Rabbit is Carrot
Baba is Cat
Cat is Rabbit
```

#### 실행결과 2

```py
Carrot
Cat
Rabbit
```

<br>

### ⌨️ 문제 풀이

1.  Baba에 명령을 한 번 이상 적용한 결과로 나올 수 있는 결과를 뽑아야하는 문제이다.
2.  그래프 탐색을 해야하는데, 문자열로 이루어진 노드로 구성된 그래프를 만들어야 하기 때문에 딕셔너리 타입을 사용해 그래프를 만들어야 한다.  
    **어떤 사물 p에 명령을 한 번 이상 적용한 결과로 다시 p가 나오는 경우는 없다.** 라는 조건이 있기 때문에 단방향 그래프를 만들어주면 된다.
3.  만든 그래프를 BFS 로 탐색하면 되는데, **Baba 에 명령을 한 번 이상** 해야하기 때문에 큐에는 Baba를 넣어 탐색을 시작한다.
4.  딕셔너리에 해당 키가 없을 수 있기 때문에 try - except 문을 사용하여 예외처리를 해준다.

<br>

### 🖥 소스 코드

```py
from collections import deque
from sys import stdin

graph = {}
for _ in range(int(stdin.readline())):
    a, b = stdin.readline().rstrip().split(' is ')

    if a not in graph:
        graph[a] = [b]
    else:
        graph[a].append(b)


def solve():
    q = deque()
    q.append("Baba")
    visited = {}
    while q:
        now = q.popleft()
        try:
            for i in graph[now]:
                if i not in visited:
                    visited[i] = 1
                    q.append(i)
        except:
            pass

    return visited


try:
    ans = sorted(solve())
    print(*ans, sep='n')

except:
    pass
```

<br>

### 💾 느낀점

1.  숫자가 아닌 문자열로 이루어진 그래프를 만들고, 탐색하는 법