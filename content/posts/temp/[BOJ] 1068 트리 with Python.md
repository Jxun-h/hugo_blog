---
author: ["Jxun-h"]
title: "[BOJ] 1068 트리 with Python"
date: "2022-07-07"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1068" target="_blank">BOJ 1068 트리</a>

<br>

### 💡 조건

1.  트리에서 리프 노드란, 자식의 개수가 0인 노드를 말한다.

2.  트리가 주어졌을 때, 노드 하나를 지울 것이다. 그 때, 남은 트리에서 리프 노드의 개수를 구하는 문제.  
    노드를 지우면 그 노드와 노드의 모든 자손이 트리에서 제거된다.

3.  다음과 같은 트리가 있다고 하자.

4.  현재 리프 노드의 개수는 3개이다. (초록색 색칠된 노드) 이때, 1번을 지우면, 다음과 같이 변한다.  
    검정색으로 색칠된 노드가 트리에서 제거된 노드이다.  
    이제 리프 노드의 개수는 1개이다.

5.  첫째 줄에 트리의 노드의 개수 N이 주어진다. N은 50보다 작거나 같은 자연수이다.  
    둘째 줄에는 0번 노드부터 N-1번 노드까지, 각 노드의 부모가 주어진다.  
    만약 부모가 없다면 (루트) -1이 주어진다. 셋째 줄에는 지울 노드의 번호가 주어진다.

6.  **BFS, 그래프탐색** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5
-1 0 0 1 1
2
```

#### 실행결과

```py
2
```

<br>

### ⌨️ 문제 풀이

1.  n개의 노드를 가진 edge 리스트를 만들어 -1 로 초기화해 부모노드가 없는 상태로 초기화 한다.

2.  0부터 n까지 순회하면서(i), 0번 노드부터 N-1번 노드까지 각 노드의 부모의 값이 0보다 같거나 크고, 삭제할 노드의 번호와 같지 않다면  
    그래프에 i를 추가한다.

3.  만약 (2)번 조건에 해당하지 않는다면 root 리스트에 i를 추가한다.  
    그 후, edge[k]를 -1 로 변경해 삭제처리를 해준다.

4.  root 리스트가 빌 때까지 while 문을 반복한다.

5.  root 에서 pop() 한 노드번호를 방문한 적이 없다면 방문처리를 해주고, edge[n]의 길이가 1일 경우 ans += 1 해준다.

6.  (5)번 조건에 해당하지 않는다면 sub = edge[n]이며, sub의 가장 왼쪽에서 데이터를 pop 한 뒤, sub 를 순회하면서 root에 i 를 추가한다.

<br>

### 🖥 소스 코드

```py
import sys
n = int(sys.stdin.readline())
stack = list(map(int, sys.stdin.readline().split()))
edge = [[-1] for _ in range(n)]

k = int(sys.stdin.readline())
root = []

for i in range(n):
    if stack[i] >= 0 and i != k:
        edge[stack[i]].append(i)
    elif stack[i] == -1 and i != k:
        root.append(i)

edge[k] = [-1]
ans = 0

visited = [0]*n

while root:
    n = root.pop()

    if visited[n] == 0:
        visited[n] = 1
        if len(edge[n]) == 1:
            ans += 1

        else:
            sub = edge[n]
            sub.pop(0)

            for i in sub:
                root.append(i)

print(ans)
```
