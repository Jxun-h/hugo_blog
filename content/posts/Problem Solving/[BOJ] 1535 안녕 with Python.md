---
author: ["Jxun-h"]
title: "[BOJ] 1535 안녕 with Python"
date: "2022-01-10"
description: ""
summary: ""
tags: ["자료구조", "PS", "배낭 알고리즘", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1535" target="_blank">BOJ 1535 안녕</a>

<br>

### 💡 조건

1.  첫째 줄에 사람의 수 `N(≤ 20)`.
2.  둘째 줄에 각각의 사람에게 인사를 할 때, 잃는 체력이 1번 사람부터 순서대로 입력.
3.  셋째 줄에는 각각의 사람에게 인사를 할 때, 얻는 기쁨이 1번 사람부터 순서대로 입력.
4.  **체력과 기쁨은 100보다 작거나 같은 자연수 또는 0.**
5.  세준이가 얻을 수 있는 최대 기쁨을 출력.
6.  **브루트포스 알고리즘, 배낭 알고리즘 유형** 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3
1 21 79
20 30 25
```

#### 실행결과

```py
50
```

<br>

### ⌨️ 문제 풀이

1.  `브루트포스 알고리즘` 혹은 `냅색 알고리즘` 으로 풀이할 수 있다.  
    나는 `냅색 알고리즘`을 사용했다.
2.  인사를 할 때 사용하는 스테미너 소모하는 리스트를 `stamina_consum` 에 `[0]`에 연결하여 저장한다.  
    인사를 할 때 얻을 수 있는 기쁨 리스트를 `get_pleasure` 에 `[0]`에 연결하여 저장한다.
3.  dp 배열을 만든다.
    -   `1명부터 n명`까지 인사를 했을 때, 얻을 수 있는 최대의 기쁨의 값을 저장할 배열.
    -   `i`번째 사람에게 인사를 하고, 스테미너 소모량보다 체력 `j`가 클 때 인사를 해서 얻을 수 있는 기쁨의 양을 계산하여 dp에 저장한다.
    -   체력이 1이 기준이며, 출력할 때 `dp[n][100]`을 출력하면 세준이가 인사를 하다 죽어버린 경우이니 오답이다. `dp[n][99]`를 출력한다.
    -   만약 `stamina[i]` 보다 체력 `j` 가 적을 경우, `dp[i][j]` 는 `dp[i-1][j]`의 값을 가져다 넣는다.
    -   그렇지 않은 경우에는 `dp[i-1][j]` 와 `dp[i-1][j - stamina_consum[i]]` 에 `get_pleasure[i]` 값 중 큰 걸 집어 넣는다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
stamina_consum = [0] + list(map(int, stdin.readline().split()))
get_pleasure = [0] + list(map(int, stdin.readline().split()))

dp = [[0] * 101 for _ in range(n + 1)]

for i in range(1, n + 1):
    for j in range(1, 101):
        if stamina_consum[i] <= j:
            dp[i][j] = max(dp[i-1][j], dp[i-1][j - stamina_consum[i]] + get_pleasure[i])
        else:
            dp[i][j] = dp[i-1][j]

print(dp[n][99])
```

<br>

### 💾 느낀점

1.  냅색 알고리즘은 풀어도 풀어도 헷갈린다.
2.  알고리즘을 알고서 풀어도 어렵고, 까먹으면 답도 없는 것 같다.
3.  냅색 알고리즘 문제를 정리해서 풀어봐야할 것 같다.
4.  문제 풀이 해설을 쓰면서도 헷갈려서 다시 인터넷을 보고 찾아서 이해하고 문제를 해석해서 썼다.