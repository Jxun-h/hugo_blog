---
author: ["Jxun-h"]
title: "[BOJ] 15486 퇴사 2 with Python"
date: "2021-08-29"
description: ""
summary: ""
tags: ["DP", "PS", "다이나믹프로그래밍", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/15486" target="_blank">BOJ 15486 퇴사 2</a>

<br>

### 💡 조건 및 풀이

1.  퇴사가 남은 일 수 `N`.
2.  `1 <= N <= 1500000`
3.  T, P 의 길이는 N과 같으며, `1 <= Ti <= 50`, `1 <= Pi <= 1000`
4.  `N + 1` 에 해당하는 날짜부터는 **상담을 할 수 없다.**
5.  **DP 유형의 문제**
6.  상담을 통해 취한 이익 중, 가장 큰 값을 반환하는 문제.

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
10
5 50
4 40
3 30
2 20
1 10
1 10
2 20
3 30
4 40
5 50
```

#### 실행결과

```
90
```python

<br>

### ⌨️ 문제 풀이

1.  편한 계산을 위해 dp를 `n + 1`의 크기만큼 생성했다.
2.  **상담을 하는데 필요한 시간을 담을 리스트** `T`를 생성
3.  **상담을 하면 얻을 수 있는 이익을 담을 리스트** `P`를 생성
4.  1일째부터 상담을 진행하면 얻을 수 있는 이익을 DP 리스트에 최댓값으로 갱신
5.  **상담을 시작한 날의 이익의 데이터가 DP 리스트의 상담이 끝나는 날 위치에 들어감**
6.  i번째 날에 상담을 시작했으면, `i + t[i]` 가 n을 넘지 말아야한다.  
    즉, 7(N)일 남은 퇴사 예정자가 퇴사 하루 전 날(i = 7)에  
    `T[i]` 2일 걸릴 상담을 시작하면, 끝내지 못하기에(N < Ti + i) 이익을 취할 수 없다.
7.  k 라는 변수를 만들어, `dp[i]`와 k 중 가장 큰 값을 집어넣는다.  
    이 값과 `dp[i + t[i]]` 이 값을 비교하여 큰 값을 `dp[i + t[i]]`에 넣는다.

<br>

### 🖥 소스 코드

```python
from sys import stdin

n = int(stdin.readline())
t, p = [], []
dp = [0 for _ in range(n + 1)]

for _ in range(n):
    ti, pi = map(int, stdin.readline().split())
    t.append(ti)
    p.append(pi)

k = 0
for i in range(n):
    k = max(k, dp[i])
    if i + t[i] > n:
        continue
    dp[i + t[i]] = max(k + p[i], dp[i + t[i]])

print(max(dp))
```

<br>

### 💾 느낀점

-   다이나믹 프로그래밍 문제에 매우 약하다. 여러 문제를 꾸준히 풀어봐야겠다.
-   다이나믹 프로그래밍 부분에서는 구현 부분에서 굉장히 헤매는 것 같다.  
    각 변수의 사용처, 갱신 등을 더 꼼곰히 체크해서 사고하는 능력을 더 키워야겠다.