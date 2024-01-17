---
author: ["Jxun-h"]
title: "[BOJ] 17521 Byte Coin with Python"
date: "2021-09-12"
description: ""
summary: ""
tags: ["그리디", "PS", "구현", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/17521" target="_blank">BOJ 17521 Byte Coin</a>

<br>

## 💡 조건 및 풀이

1.  주식 시장에서 단타를 치는 국제자본 부동산 회사를 도와 최고의 수익을 내는 문제.
2.  일 수를 나타내는 `1 <= n <= 15`
3.  초기 현금을 나타내는 `W`
4.  다음 `n` 개의 줄에서, `i번째 줄은 i일의 바이트 코인 가격`을 나타내는   
정수 `si`가 주어진다`(1 ≤ si ≤ 50)`.
5.  **단순 구현, 그리디 알고리즘 문제**

<br>

## 🔖 예제 및 실행결과

#### 예제

```
10 24
5
7
5
4
2
7
8
5
3
4
```

#### 실행결과

```
170
```

<br>

## ⌨️ 문제 풀이

1.  현재 매수한 코인이 있는지의 상태를 체크할 수 있는 변수 `"m" (기본값은 False)`  
    코인을 몇개 샀는지에 대한 정보를 넣어줄 변수 `"coin"`
2.  코인이 다음 날에 가격이 상승하거나 변동이 없다?  
    이미 매수한 경우, `pass`  
    매수하지 않은 경우, `구매`
3.  코인이 다음 날에 가격이 떨어진다?  
    `판매`
4.  최종적으로 남아 있는 현금을 출력

<br>

## 🖥 소스 코드

```python
from sys import stdin
n, w = map(int, stdin.readline().split())
arr = []
for _ in range(n):
    arr.append(int(stdin.readline()))

m = False
coin = 0
for i in range(n - 1):
    if not m and arr[i] < arr[i + 1]:
        m = arr[i]
        coin = w // m
        w -= coin * m

    elif m and arr[i] > arr[i + 1]:
        w += arr[i] * coin
        coin, m = 0, False

if m:
    w += coin * arr[-1]

print(w)
```

<br>

## 💾 느낀점

-   단순 구현 및 그리디 문제였습니다.
-   코인을 샀는지 안샀는지에 대한 변수를 추가하여 쉽게 풀 수 있었습니다.
-   실제 코인 시장이나 은행처럼 x% 수익률 계산했다가 큰 코 다칠뻔했습니다.
-   문제를 더 확실히 읽고 압축하는 능력을 키워야겠습니다.