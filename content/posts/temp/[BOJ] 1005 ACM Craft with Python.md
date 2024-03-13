---
author: ["Jxun-h"]
title: "[BOJ] 1005 ACM Craft with Python"
date: "2022-07-17 22:33:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "BFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1005" target="_blank">BOJ 1005 ACM Craft</a>

<br>

### 💡 조건

1.  서기 2012년! 드디어 2년간 수많은 국민들을 기다리게 한 게임 ACM Craft (Association of Construction Manager Craft)가 발매되었다.

2.  이 게임은 지금까지 나온 게임들과는 다르게 ACM크래프트는 다이나믹한 게임 진행을 위해 건물을 짓는 순서가 정해져 있지 않다.  
    즉, 첫 번째 게임과 두 번째 게임이 건물을 짓는 순서가 다를 수도 있다.  
    **매 게임시작 시 건물을 짓는 순서가 주어진다. 또한 모든 건물은 각각 건설을 시작하여 완성이 될 때까지 Delay가 존재한다.**

<br>
<center><img src='/1005_1.png' /></center>
<br>

3.  프로게이머 최백준은 애인과의 데이트 비용을 마련하기 위해 서강대학교배 ACM크래프트 대회에 참가했다!  
    최백준은 화려한 컨트롤 실력을 가지고 있기 때문에 모든 경기에서 특정 건물만 짓는다면 무조건 게임에서 이길 수 있다.

4.  매 게임마다 특정건물을 짓기 위한 순서가 달라지므로 최백준은 좌절하고 있었다.  
    백준이를 위해 특정건물을 가장 빨리 지을 때까지 걸리는 최소시간을 알아내는 문제.

5.  첫째 줄에는 테스트케이스의 개수 T가 주어진다.  
    첫째 줄에 건물의 개수 N과 건물간의 건설순서 규칙의 총 개수 K이 주어진다. (건물의 번호는 1번부터 N번까지 존재한다)

6.  둘째 줄에는 각 건물당 건설에 걸리는 시간 D1, D2, ..., DN이 공백을 사이로 주어진다.  
    셋째 줄부터 K+2줄까지 건설순서 X Y가 주어진다. (이는 건물 X를 지은 다음에 건물 Y를 짓는 것이 가능하다는 의미이다)  
    마지막 줄에는 백준이가 승리하기 위해 건설해야 할 건물의 번호 W가 주어진다.

7.  2 ≤ N ≤ 1000  
    1 ≤ K ≤ 100,000  
    1 ≤ X, Y, W ≤ N  
    0 ≤ Di ≤ 100,000, Di는 정수

8.  **BFS, 그래프탐색** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
2
4 4
10 1 100 10
1 2
1 3
2 4
3 4
4
8 8
10 20 1 5 8 7 1 43
1 2
1 3
2 4
2 5
3 6
5 7
6 7
7 8
7
```

#### 실행결과

```py
120
39
```

<br>

### ⌨️ 문제 풀이

1.  문제를 요약해보자면, 아래와 같다.
    -   각 테스트 케이스마다 건물을 지을 수 있는 순서는 다르다.
    -   백준이가 이기기 위해서는 특정 건물을 지어야 승리가 가능하다.
    -   특정 건물을 짓기 위해서는 선행되는 건물을 지을 필요가 있다.

2.  간단하게 정리를 해보면 우리는 **건설순서가 정해져 있는 건물을 차례로 건설하면서, W번 건물을 지을 때까지의 최소 시간을 구해야한다.**  
    이러한 문제에 사용할 수 있는 알고리즘은 위상정렬인데, 위상정렬의 개념고 위에 써놓은 것과 개념이 크게 다르지 않다.  
    **위상정렬이란, 순서가 정해져있는 작업을 차례로 수행해야할 때 그 순서를 결정해주기 위해서 사용하는 알고리즘이다.**

3.  건물의 개수 N과 건물간의 건설순서 규칙의 총 개수 K 를 입력받아, 위상정렬 알고리즘에 필요한 indegree 리스트를 n + 1 개 만들어준다.  
    또한 N + 1개의 노드를 가진 그래프도 생성한다.  
    각 건물을 건설하는데에 필요한 시간을 입력받은 후, 건설순서를 입력받아 그래프에 입력한다.  
    만약 a, b를 입력 받았다면, graph[a].append(b) 이며 indegree[b] += 1 이다.  
    **b 건물을 건설하기 위해서는 a 건물을 건설해야한다는 뜻이기 때문에** +1 이 되는 것이다.

4.  이후, W 를 입력받아 위상정렬 알고리즘의 로직이 있는 topology_sort() 함수에 W를 넘겨준다.  
    위상정렬 알고리즘에서는, indegree 리스트에서의 값이 0인 것을 q에 먼저 넣고 처리를 한다.  
    indegree 리스트에서의 값은 해당 건물이 지어지기 위해서는 먼저 지어져야할 건물이 있다는 것을 의미하기 때문이다.

5.  위상정렬 함수에서는 DP 리스트를 만들어 사용자가 어떤 건물을 지었을 때의 소요시간을 체크한다.  
    큐에서 뺀 건물 번호(now) 를 기준으로 그래프를 따라 순회하면서, 순회하는 건물의 번호(node)에 해당하는 indegree의 값을 1씩 빼준다.  
    그리고 DP[node] 에 해당하는 값을 DP[now] + 건설에 필요한 시간[node] 값과 비교해 가장 큰 값으로 갱신한다.

6.  이후, indegree[node] 의 값이 0 이라면 queue에 추가하고 반복한다.  
    queue 가 모두 빌 때까지 순회를 마쳤다면, DP[W] 의 값을 반환하고 출력한다.  
    DP[W]의 값은 W 번 건물이 지어지는 최소 시간을 의미한다.

<br>

### 🖥 소스 코드

```py
from collections import deque
from sys import stdin


def topology_sort(w):
    q = deque()
    dp = [0 for _ in range(n + 1)]
    for i in range(1, n + 1):
        if indegree[i] == 0:
            q.append(i)
            dp[i] = arr[i]

    while q:
        now = q.popleft()

        for node in graph[now]:
            indegree[node] -= 1
            dp[node] = max(dp[now] + arr[node], dp[node])
            if indegree[node] == 0:
                q.append(node)

    return dp[w]


for tc in range(int(stdin.readline())):
    n, m = map(int, stdin.readline().split())
    indegree = [0] * (n + 1)
    graph = [[] for _ in range(n + 1)]
    arr = [0] + list(map(int, stdin.readline().split()))
    for _ in range(m):
        a, b = map(int, stdin.readline().split())
        graph[a].append(b)
        indegree[b] += 1

    w = int(stdin.readline())
    print(topology_sort(w))
```

<br>

### 💾 느낀점

1.  위상정렬이란, 순서가 정해져있는 작업을 차례로 수행해야할 때 그 순서를 결정해주기 위해서 사용하는 알고리즘.  
    이를 어떻게 사용하고, 응용해야할지 더 연습이 필요할 것 같다. 복잡해보이지만, 개념과 필요한 상황을 잘 이해한다면  
    충분히 잘 사용할 수 있을 것 같은 느낌이다.