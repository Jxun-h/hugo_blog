---
author: ["Jxun-h"]
title: "[Programmers] 거리두기 확인하기 with Python"
date: "2021-08-29"
description: ""
summary: ""
tags: ["BFS", "PS", "너비우선탐색", "알고리즘", "프로그래머스"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---
<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/81302" target="_blank">Programmers - 거리두기 확인하기</a>

<br>

### 💡 조건 및 풀이

1.  대기실에 응시자들이 면접을 위해 대기를 하고 있다. 대기실에 있는 대기자들이 거리 두기를 잘 지키고 있을까?
2.  대기실은 5개, 각 대기실은 `5 * 5`의 크기입니다.
3.  응시자들 간의 거리는 맨해튼 거리는 2 이하로 앉을 수 없으니 3 이상이어야한다.
4.  맨해튼 거리가 2이하여도 응시자 사이에 파티션으로 막혀 있으며 지나갈 다른 방법으로 응시자로의 경로가 없다면 상관이 없다.
5.  **BFS 유형의 문제**
6.  두 테이블 `T1, T2`가 행렬 `(r1, c1), (r2, c2)`에 각각 위치하고 있다면,  
    `T1, T2` 사이의 맨해튼 거리는 `|r1 - r2| + |c1 - c2|`
7.  응시자, 테이블, 파티션 = `P`, `O`, `X`
8.  **정확성 테스트의 시간은 10초.**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
places = [["POOOP", "OXXOX", "OPXPX", "OOXOX", "POXXP"], ["POOPX", "OXPXP", "PXXXO", "OXXXO", "OOOPP"], ["PXOPX", "OXOXP", "OXPOX", "OXXOP", "PXPOX"], ["OOOXX", "XOOOX", "OOOXX", "OXOOX", "OOOOO"], ["PXPXP", "XPXPX", "PXPXP", "XPXPX", "PXPXP"]]
```

#### 실행결과

```python
[1, 0, 1, 1, 1]
```

<br>

### ⌨️ 문제 풀이

1.  정확성 테스트가 있기 때문에 시간초과 및 메모리 초과에 신경을 써야한다.  
    그러므로 응시자들의 좌표만 따로 배열로 받아서 맨해튼 거리를 구한 뒤 맨해튼 거리가 2 이하인 것들만 BFS를 통해  
    응시자 사이가 파티션으로 막혀 있는지 확인한다.
2.  대기실을 BFS로 돌면서 큐에 `이동 거리, 좌표, 움직인 이동 좌표`를 배열로 넣어 주며,  
    이동 거리가 맨해튼 거리보다 멀다면 BFS 과정을 skip 한다.
3.  두 응시자의 맨해튼 거리가 2 이하일 때, 사이에 파티션이 있는 경우를 처리 하지 못해서 테스트 케이스 5번이 틀렸다.  
    내가 틀린 반례는 아래와 같다. 답은 1이다.
    
    ```python
    [["OPXPO", "OOOOO", "OOOOO", "OOOOO", "OOOOO"]]   
    ```
    
<br>

### 🖥 소스 코드

```python
from collections import deque

dx, dy = [1, -1, 0, 0], [0, 0, -1, 1]


def bfs(board, now, goal, dist):
    q = deque()
    visited = []
    x, y = now
    q.append((0, x, y, []))
    visited.append(now)
    check = False

    while q:
        cost, x, y, visit = q.popleft()

        # 움직인 거리가 맨헤튼 거리보다 많으면 넘어가기
        if cost > dist:
            continue

        if (x, y) == goal:
            for i, j in visit:
                if board[i][j] == 'X':
                    check = True
                elif board[i][j] == 'O':
                    return False

        for i in range(4):
            nx, ny = dx[i] + x, y + dy[i]
            if -1 < nx < 5 and -1 < ny < 5:
                if (nx, ny) not in visited:
                    # 목표 지점을 visited 에 넣지 않는다.
                    # 가능한 많은 경로를 염두에 두어 계산한다.
                    if (nx, ny) != goal:
                        visited.append((nx, ny))
                    temp = visit[:]
                    temp.append((nx, ny))
                    q.append((cost + 1, nx, ny, temp))
    return check


def solution(places):
    answer = []

    for i in range(len(places)):
        board = []
        data = places[i]

        ps = []

        # 대기실 리스트 만들기
        for j in range(5):
            for k in range(5):
                if data[j][k] == 'P':
                    ps.append((j, k))
            board.append(list(data[j]))

        ps.sort()
        check = True
        for j in range(len(ps)):
            x1, y1 = ps[j]
            for k in range(j + 1, len(ps)):
                x2, y2 = ps[k]
                dist = abs(x1 - x2) + abs(y1 - y2)
                if dist < 3:
                    if not bfs(board, ps[j], ps[k], dist):
                        check = False
                        break
            if not check:
                break

        answer.append(1) if check else answer.append(0)

    return answer
```

<br>


### 💾 느낀점

-   어제 풀었던 불! 보다 쉬웠다.
-   반례 테스트 케이스를 찾는데 조금 어려움이 있었다.
-   BFS는 짜기 나름인 것 같다. queue 에 넣는 정보를 다양하게 사용하는 법이 익숙해지고 있는 것 같아 좋다.  
    그러나 visited 배열을 더 다양하게 사용하는 법을 연습해야겠다.