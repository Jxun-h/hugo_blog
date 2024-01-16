---
author: ["Jxun-h"]
title: "[Programmers] 합승 택시 요금 with Python"
date: "2021-08-29"
description: ""
summary: ""
tags: ["플로이드-와샬", "PS", "그래프이론", "알고리즘", "프로그래머스"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/72413" target="_blank">Programmers - 합승 택시 요금</a>

<br>

### 💡 조건 및 풀이

1.  노드의 개수 `n`, 출발노드 `s`, A의 도착지점 `a`,  
    B의 도착지점 `b`, 노드 간 이동하는데 드는 비용 `fares`
2.  A와 B가 서로 다른 목적지를 향하고 있다.
3.  **A와 B가 따로 이동하는 것**과 **어느 지점까지 같이 이동하는 것** 중에  
    최소 비용을 구하는 문제
4.  미로의 벽에 붙어있으면 탈출이 가능하다.

<br>

### 🔖 예제 및 실행결과

#### 예제

```
print(solution(6, 4, 6, 2, [[4, 1, 10], [3, 5, 24], [5, 6, 2], [3, 1, 41], [5, 1, 24], [4, 6, 50], [2, 4, 66], [2, 3, 22], [1, 6, 25]]))

print(solution(7, 3, 4, 1, [[5, 7, 9], [4, 6, 4], [3, 6, 1], [3, 2, 3], [2, 1, 6]]))

print(solution(6, 4, 5, 6, [[2, 6, 6], [6, 3, 7], [4, 6, 7], [6, 5, 11], [2, 5, 12], [5, 3, 20], [2, 4, 8], [4, 3, 9]]))
```

#### 실행결과

```
82
14
18
```

<br>

### ⌨️ 문제 풀이

1.  거리 정보를 담을 graph 2중 리스트를 생성
2.  `플로이드 와샬 알고리즘`을 사용하여 각각 노드끼리 얼마의 비용이 드는지 계산  
    **`i에서 j로 가는 비용`과 `i에서 k를 경유하여 j로 가는 비용` 중에 더 저렴한 것**
3.  `answer`를 더 저렴한 비용을 비교하기 위해 1e9로 초기화
4.  for 문으로 1번 노드부터 n번 노드까지 아래의 내용을 검사한다.  
    `answer`와 **`출발지(s)에서 i까지 합승한 값` + `i 부터 B의 목적지까지 가는 값` + `i 부터 A의 목적지까지 가는 값`** 비교

<br>

### 🖥 소스 코드
```python
from collections import deque


def solution(n, s, a, b, fares):
    answer = int(1e9)
    INF = int(1e9)
    distance = [[INF] * (n + 1) for _ in range(n + 1)]
    for q, w, e in fares:
        distance[q][w] = e
        distance[w][q] = e

    for k in range(1, n + 1):
        for i in range(1, n + 1):
            for j in range(1, n + 1):
                if i == j:
                    distance[i][j] = 0
                else:
                    if distance[i][j] > distance[i][k] + distance[k][j]:
                        distance[i][j] = distance[i][k] + distance[k][j]

    for i in range(1, n + 1):
        if answer > distance[s][i] + distance[i][b] + distance[i][a]:
            answer = distance[s][i] + distance[i][b] + distance[i][a]

    return answer
```

<br>

### 💾 느낀점

-   `BFS`로 최단거리를 찾아보기 위해 이동거리 값을 저장하는 큐를 생성해 문제를 풀려고 시도했다.  
    그 결과 시간을 매우 낭비하게 되었고, `플로이드 와샬`을 떠올려 문제 풀이를 했다.
-   `플로이드 와샬 구현 방법을 조금 헷갈리는 문제점`이 있었다.  
    `플로이드 와샬`이면 굳이 `BFS`가 없는데 위에서 말한 `BFS` 소스코드를 그대로 두었었다.
-   `시간초과`가 났다. 26번 테스트 케이스에서 시간초과가 났다.  
    플로이드 와샬 부분과 반환할 **answer를 위해 비교하는 부분에서 min() 대신  
    if를 써주었더니 속도차이가 두 배 가까이 났다.**

