---
author: ["Jxun-h"]
title: "[BOJ] 20546 🐜 기적의 매매법 🐜 with Python"
date: "2021-12-18"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "스택", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/20546" target="_blank">BOJ 20546 🐜 기적의 매매법 🐜</a>

<br>

### 💡 조건

1.  모든 거래는 전량 매수와 전량 매도로 이루어진다.
    -   현재 가지고 있는 현금이 100원이고 주가가 11원이라면 99원어치의 주식을 매수하는 것이다.
    -   단, 현금이 100원 있고 주가가 101원이라면 주식을 살 수 없다.
    -   성민이는 빚을 내서 주식을 하지는 않는다.
2.  3일 연속 가격이 전일 대비 상승하는 주식은 다음날 무조건 가격이 하락한다고 가정한다.
    -   따라서 현재 소유한 주식의 가격이 3일째 상승한다면, 전량 매도한다.
    -   전일과 오늘의 주가가 동일하다면 가격이 상승한 것이 아니다.
3.  3일 연속 가격이 전일 대비 하락하는 주식은 다음날 무조건 가격이 상승한다고 가정한다.
    -   따라서 이러한 경향이 나타나면 즉시 주식을 전량 매수한다.
    -   전일과 오늘의 주가가 동일하다면 가격이 하락한 것이 아니다.
4.  1월 14일의 자산은 (현금 + 1월 14일의 주가 × 주식 수)로 계산한다.
5.  1월 14일 기준 준현이의 자산이 더 크다면 "BNP"를, 성민이의 자산이 더 크다면 "TIMING"을 출력한다.
6.  **Stack, 자료구조 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
100
10 20 23 34 55 30 22 19 12 45 23 44 34 38
```

#### 실행결과

```py
BNP
```

<br>

### ⌨️ 문제 풀이

1.  문제에서 요구한 33 매매법의 세가지 룰을 먼저 정리하고 구현을 하면 좋습니다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

m = int(stdin.readline())
arr = list(map(int, stdin.readline().split()))
jm, sm, j, s, status = m, m, 0, 0, [0, '']
yesterday = arr[0]


for i in range(14):
    # 준현
    if jm // arr[i] != 0:
        temp = jm // arr[i]
        j += (jm // arr[i])
        jm -= temp * arr[i]

    # 성민
    change = 0
    if yesterday < arr[i]:
        if status[1] == '-':
            change = 1
        status[1] = '+'

    elif yesterday > arr[i]:
        if status[1] == '+':
            change = 1
        status[1] = '-'

    yesterday = arr[i]

    if change:
        status[0] = 1
    elif status[1] != '':
        status[0] += 1

    if status[0] >= 3:
        if status[1] == '+':
            if sm // arr[i] != 0:
                sm += s * arr[i]
                s = 0

        if status[1] == '-':
            temp = sm // arr[i]
            s += (sm // arr[i])
            sm -= temp * arr[i]


last_day = arr[-1]
sm += (s * last_day)
jm += (j * last_day)

if sm == jm:
    print("SAMESAME")
elif sm > jm:
    print("TIMING")
else:
    print("BNP")
```

<br>

### 💾 느낀점

1.  단순한 구현문제였다.
2.  문제를 잘 읽고 문제를 압축하고 정리하는 연습이 필요하겠다.