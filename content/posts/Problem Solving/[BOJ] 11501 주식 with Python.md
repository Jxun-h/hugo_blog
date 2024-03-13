---
author: ["Jxun-h"]
title: "[BOJ] 11501 주식 with Python"
date: "2022-02-24"
description: ""
summary: ""
tags: ["자료구조", "PS", "그리디", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/11501" target="_blank">BOJ 11501 주식</a>

<br>

### 💡 조건

1.  홍준이는 요즘 주식에 빠져있다. 아래 세가지 중 하나의 행동을 한다.
    -   주식 하나를 산다.
    -   원하는 만큼 가지고 있는 주식을 판다.
    -   아무것도 안한다.
2.  테스트케이스 수를 나타내는 자연수 T.
3.  테스트케이스 별로 첫 줄에는 날의 수를 나타내는 자연수 N(2 ≤ N ≤ 1,000,000)이 주어지고,  
    둘째 줄에는 날 별 주가를 나타내는 N개의 자연수들이 공백으로 구분되어 순서대로 주어진다.
4.  날 별 주가는 10,000이하다.
5.  최대 이익이 얼마나 되는지 계산을 해 출력하는 문제.
6.  **그리디 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3
3
10 7 6
3
3 5 9
5
1 1 3 1 2
```

#### 실행결과

```py
0
10
5
```

<br>

### ⌨️ 문제 풀이

1.  이 문제의 키포인트는, 주식의 예측 값이 떨어질 때 주식을 모두 팔아 이익을 챙기는 것이 아닌,  
    **현재 가격의 주식을 언제 팔아서 최대 이익을 낼 것이냐?** 입니다.
2.  그러므로 입력을 받은 데이터를 역순회하면서, 현재 순회하고 있는 주가가 주가 최댓값보다 크다면 갱신합니다.
3.  순회하고 있는 주가가 주가 최댓값보다 작아지면 출력할 변수(money) 에 (주가 최댓값 - 현재 순회 하고 있는 주가)를 더해줍니다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

for tc in range(int(stdin.readline())):
    n = int(stdin.readline())
    days = list(map(int, stdin.readline().split()))
    m_val, money = 0, 0

    for i in range(n - 1, -1, -1):
        if m_val < days[i]:
            m_val = days[i]

        elif m_val > days[i]:
            money += (m_val - days[i])

    print(money)
```

<br>

### 💾 느낀점

1.  그리디라고 무지성으로 그냥 더했다 팔았다 하는게 아니라 역순으로도 생각해볼 수 있게 도와준 문제였습니다.
2.  그리디도 쉽게 볼게 아니었습니다. 생각이 많이 열려있지 않다는 걸 느꼈습니다.