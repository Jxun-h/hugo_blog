---
author: ["Jxun-h"]
title: "[BOJ] 9663 N-Queen with Python"
date: "2022-02-14"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "백트래킹", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/9663" target="_blank">BOJ 9663 N-Queen</a>

<br>

### 💡 조건

1.  N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제.
2.  1 <= N < 15
3.  **브루트포스, 백트래킹 알고리즘**유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
8
```

#### 실행결과

```py
92
```

<br>

### ⌨️ 문제 풀이

1.  퀸은 각 줄마다 반드시 하나씩 들어가야한다.
2.  퀸이 있는 자리 기준으로 대각선, 세로선에는 다른 퀸이 존재할 수 없다.
3.  퀸의 좌표를 하나하나 확인하면서 문제를 해결하려고 하면 시간초과가 난다.
4.  dfs 함수에서 퀸을 놓은 개수가 n개가 되었으면 res + 1 후 return한다.
5.  (2)번의 기준에 따라, a는 세로줄, b, c는 대각선을 체크해주는 리스트이다.  
    n의 길이만큼 순회하면서 a, b, c 리스트의 인덱스에 해당하는 값이 하나라도 True 일 경우
6.  퀸을 놓지 못하는 자리이기 때문에 continue  
    a, b, c 리스트의 인덱스에 해당하는 값이 모두 False 인 경우, 모두 True 로 갱신한 뒤 dfs(x + 1) 재귀호출
    
7.  빠져나온 후에는 백트래킹을 위해 a, b, c 리스트의 인덱스에 해당하는 부부을 False로 갱신


<br>

### 🖥 소스 코드

```py
from sys import stdin

a, b, c = [False for _ in range(15)], [False for _ in range(30)], [False for _ in range(30)]
n = int(stdin.readline())
res = 0


def dfs(x):
    global res
    if x == n:
        res += 1
        return

    for y in range(n):
        if a[y] or b[x + y] or c[x + (n - y)]:
            continue

        a[y] = True
        b[x + y] = True
        c[x + (n - y)] = True

        dfs(x + 1)

        a[y] = False
        b[x + y] = False
        c[x + (n - y)] = False


dfs(0)
print(res)
```

<br>

### 💾 느낀점

1.  백트래킹의 대표적인 문제라고 하지만, 대표적으로 어려운 문제라고 하는게 맞는 것 같다.
2.  대각선과 세로의 각 좌표를 일일히 검사하려고 해서 시간초과를 피하지 못했다.
3.  풀이를 보고 일차원 리스트를 세 개 만들어 검사하는 것을 보고, 놀랐던 기억이 있다.
4.  문제를 포스팅하면서 다시 한 번 풀이를 생각해보는 것이 큰 도움이 되었다.