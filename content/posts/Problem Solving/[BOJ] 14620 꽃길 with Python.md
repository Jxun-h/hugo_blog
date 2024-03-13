---
author: ["Jxun-h"]
title: "[BOJ] 14620 꽃길 with Python"
date: "2021-12-13"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/14620" target="_blank">BOJ 14620 꽃길</a>

<br>

### 💡 조건

1.  꽃밭은 `N * N` 의 격자 모양이고, 씨앗을 `(1, 1) ~ (N, N)`의 지점 중 한곳에 심을 수 있다.  
    1년 후 상하좌우로 꽃잎이 펼쳐진다.
2.  어떤 씨앗이 꽃이 핀 뒤, 다른 꽃잎 혹은 꽃술과 닿게 될 경우 꽃이 둘 다 죽어버린다.
3.  서로 다른 **세 씨앗**을 모두 꽃이 피게하면서 가장 싼 가격에 화단을 대여하려고 한다.  
    **진아가 꽃을 심을 수 있는 최소비용을 구하는 문제이다.**
4.  한 변의 길이 N`(6 ≤ N ≤ 10)`
5.  화단의 지점당 가격`(0 ≤ G ≤ 200)`
6.  **브루트포스 알고리즘 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
6
1 0 2 3 3 4
1 1 1 1 1 1
0 0 1 1 1 1
3 9 9 0 1 99
9 11 3 1 0 3
12 3 0 0 0 1
```

#### 실행결과

```python
12
```

<br>

### 🖥 소스 코드

```python
from sys import stdin, setrecursionlimit
setrecursionlimit(10 ** 9)

n = int(stdin.readline())
arr = []
res = [int(1e9)]
visited = set()
dx, dy = [1, 0, 0, -1], [0, 1, -1, 0]

for _ in range(n):
    arr.append(list(map(int, stdin.readline().split())))


def solve(cnt, cost, v):
    if cnt == 3:
        res[0] = min(res[0], cost)

    else:
        for i in range(1, n - 1):
            for j in range(1, n - 1):
                temp_visit = set()
                temp_visit.add((i, j))
                tf = 1
                temp = arr[i][j]
                for k in range(4):
                    nx, ny = i + dx[k], j + dy[k]
                    if -1 < nx < n and -1 < ny < n:
                        if (nx, ny) not in v:
                            temp += arr[nx][ny]
                            temp_visit.add((nx, ny))
                        else:
                            tf = 0
                            break
                    else:
                        tf = 0
                        break

                if tf and temp_visit:
                    v.update(temp_visit)
                    solve(cnt + 1, cost + temp, v)
                    v -= temp_visit


solve(0, 0, visited)
print(*res)
```

<br>

### ⌨️ 문제 풀이

1.  `DFS` 알고리즘을 사용했다.
2.  **심은 씨앗이 3개가 되지 않으면, 계속 씨앗을 심어준다.**  
    전체 좌표를 순회하면서 작업을 한다. 씨앗을 심은 부분을 기준으로 상하좌우의 좌표를 `visited` 집합 자료형에 넣어주어서,  
    `visited`의 좌표들에도 씨앗을 심을 수 없게 한다.
3.  `solve(심은 씨앗의 갯수, 화단을 빌리는 비용, 꽃잎이 피어 심을 수 없는 구역들)` 에 심은 씨앗의 개수를 하나씩 늘려준다.
4.  **심은 씨앗이 3개가 된다면 최소비용인지 확인하여 res 값에 저장한다.**

<br>

### 💾 느낀점