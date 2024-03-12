---
author: ["Jxun-h"]
title: "[BOJ] 1236 성 지키기 with Python"
date: "2022-02-10"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "시뮬레이션", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1236" target="_blank">BOJ 1236 성 지키기</a>

<br>

### 💡 조건

1.  직사각형 모양의 성을 가지고 있다. 성의 1층은 몇 명의 경비원에 의해서 보호되고 있다.  
    영식이는 모든 행과 모든 열에 한 명 이상의 경비원이 있으면 좋겠다고 생각했다.
2.  성의 크기와 경비원이 어디있는지 주어졌을 때, 몇 명의 경비원을 최소로 추가해야 영식이를 만족시키는지 구하는 문제
3.  0 <= N, M <= 50
4.  성의 상태는 .은 빈칸, X는 경비원이 있는 칸이다.
5.  **구현, 시뮬레이션**유형의 문제

### 🔖 예제 및 실행결과

#### 예제

```py
4 4
....
....
....
....
```

#### 실행결과

```py
4
```

<br>

### ⌨️ 문제 풀이

1.  각 열과 행에 모두 경비원이 있었으면 좋겠다고 생각을 했으니, 열과 행에 경비원이 있는지 체크할 col, row 리스트를 생성한다.  
    이 리스트는 각 원소를 False 로 초기화 한 상태로 생성한다.
2.  경비원의 값을 저장할 r1, r2 변수를 생성한다.
3.  성의 크기만큼 순회하면서 (i, j) 에 X 가 있을 경우, row[i], col[j] 를 각각 True로 갱신한다.
4.  각 성의 가로 크기(i -> n), 세로 크기(j -> m)만큼 순회하면서 row[i], col[j] 가 각각 False 일 경우  
    r1, r2 에 각각 + 1을 더해준다.
5.  r1, r2 중 가장 큰 값을 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = map(int, stdin.readline().split())
arr = []
col = [False] * m
row = [False] * n
r1, r2 = 0, 0

for i in range(n):
    data = list(stdin.readline().rstrip())
    arr.append(data)

for i in range(n):
    for j in range(m):
        if arr[i][j] == 'X':
            row[i] = True
            col[j] = True

for i in range(n):
    if not row[i]:
        r1 += 1

for j in range(m):
    if not col[j]:
        r2 += 1

print(max(r1, r2))
```

<br>

### 💾 느낀점

1.  구현 문제이지만, 어디에 경비원이 있어야 각 열과 행이 모두 True 값을 가지는지 생각하는 것이 헷갈렸다.
2.  브론즈라고 했지만, 구현은 역시 그 이상의 티어로 봐야하는 것 같다.
3.  논리적인 사고력이 약하다는 것을 다시 한 번 느끼게 해주는 문제였다.