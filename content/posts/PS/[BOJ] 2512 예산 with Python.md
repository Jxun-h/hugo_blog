---
author: ["Jxun-h"]
title: "[BOJ] 2512 예산 with Python"
date: "2022-06-10"
description: ""
summary: ""
tags: ["자료구조", "PS", "이분탐색", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2512" target="_blank">BOJ 2512 예산</a>

<br>

### 💡 조건

1.  국가의 역할 중 하나는 여러 지방의 예산요청을 심사하여 국가의 예산을 분배하는 것이다.  
    국가예산의 총액은 미리 정해져 있어서 모든 예산요청을 배정해 주기는 어려울 수도 있다.  
    그래서 정해진 총액 이하에서 가능한 한 최대의 총 예산을 다음과 같은 방법으로 배정한다.
    1.  모든 요청이 배정될 수 있는 경우에는 요청한 금액을 그대로 배정한다.
    2.  모든 요청이 배정될 수 없는 경우에는 특정한 정수 상한액을 계산하여 그 이상인 예산요청에는 모두 상한액을 배정한다.
    3.  상한액 이하의 예산요청에 대해서는 요청한 금액을 그대로 배정한다.

2.  여러 지방의 예산요청과 국가예산의 총액이 주어졌을 때, 위의 조건을 모두 만족하도록 예산을 배정하는 문제.

3.  첫째 줄에는 지방의 수를 의미하는 정수 N이 주어진다. N은 3 이상 10,000 이하이다.

4.  다음 줄에는 각 지방의 예산요청을 표현하는 N개의 정수가 빈칸을 사이에 두고 주어진다. 이 값들은 모두 1 이상 100,000 이하이다.

5.  그 다음 줄에는 총 예산을 나타내는 정수 M이 주어진다. M은 N 이상 1,000,000,000 이하이다.

6.  **이분탐색** 유형의 문제

<br>

## 🔖 예제 및 실행결과

#### 예제

```py
4
120 110 140 150
485
```

#### 실행결과

```py
127
```

<br>

## ⌨️ 문제 풀이

1.  총 예산을 나타내는 M이 N 이상 1,000,000,000 이하이다.  
    이 큰 값을 N부터 탐색하면 시간초과가 걸리기 때문에 이분탐색을 사용해 총예산에서 상한액을 찾아주면 된다.

2.  요청한 예산들을 담은 arr 리스트의 max 값을 r, 0을 l로 두고 이분탐색을 진행한다.

3.  (l + r) // 2 값을 mid 로 두고 arr 리스트를 순회하면서 mid 값과 순회하는 값을 비교해 작은 값을 total 에 넣어준다.

4.  total 이 m 값보다 클 때는 r을 mid로 땡겨주고, 그 외의 상황일 때는 ans의 값과 비교해서 큰 값을 ans 에 저장한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
arr = list(map(int, stdin.readline().split()))
m = int(stdin.readline())
start, end = 0, max(arr)
ans = -int(1e9)

while start <= end:
    mid = (start + end) // 2

    total = 0
    for i in arr:
        total += min(i, mid)

    if total > m:
        end = mid - 1
    else:
        start = mid + 1
        ans = max(ans, mid)

print(ans)
```
