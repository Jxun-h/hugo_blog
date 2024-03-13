---
author: ["Jxun-h"]
title: "[BOJ] 22252 정보 상인 호석 with Python"
date: "2022-05-18"
description: ""
summary: ""
tags: ["자료구조", "PS", "우선순위 큐", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/22252" target="_blank">BOJ 22252 정보 상인 호석</a>

<br>

### 💡 조건

1.  관찰하면서 얻은 정보는 총 $Q$ 개이다. 각 정보는 다음의 2가지 중 하나이다.
    1.  1 Name k C_1, C_2, ..., C_k : 이름이 [Name]인 고릴라가 k 개의 정보를 얻었으며, 각 가치는 C_1 부터 C_k 이다.
    2.  2 Name b : 호석이가 이름이 [Name]인 고릴라에게 b 개의 정보를 구매한다.  
        이때 고릴라가 가진 정보들 중 가장 비싼 b 개를 구매하며, 고릴라가 가진 정보가 b개 이하이면 가진 모든 정보를 구매한다.

2.  고릴라들이 정보를 얻는 사건과 호석이가 거래하는 정보가 시간순으로 주어진다. 첫 번째 줄에는 쿼리의 개수 Q가 주어진다.

3.  Q 개의 줄에 걸쳐서 각 줄에 쿼리가 주어진다.

4.  쿼리는 1이나 2로 시작한다.  
    1로 시작하는 경우에는 정보를 얻은 정보 고릴라의 이름과 k가 주어지며 이어서  
    k개의 정보 가치 C_1, ..., C_k가 자연수로 주어진다.

5.  모든 C_i는 1 이상 100,000 이하이다.  
    2로 시작하는 경우에는 호석이가 거래하려는 정보 고릴라의 이름과 구매하려는 정보의 개수 b가 주어진다.

6.  제한사항은 아래와 같다.
    1.  1 ≤ Q ≤ 100,000, Q 는 자연수
    2.  모든 Name은 알파벳 소문자 혹은 대문자로 이루어져 있고 공백이 없으며 길이는 1 이상 15 이하이다.
    3.  1 ≤ k ≤ 100,000, k 는 자연수
    4.  1 ≤ C ≤ 100,000, C 는 자연수
    5.  1 ≤ b ≤ 100,000, b 는 자연수
    6.  모든 쿼리에 대한 k 의 합은 1,000,000 을 넘지 않는다.
7.  **자료구조, 우선순위큐, heapq** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
7
1 Cpp 5 10 4 2 8 4
1 Java 2 8 2
2 Cpp 2
1 Cpp 2 10 3
2 Cpp 3
2 Java 1
2 Python 10
```

#### 실행결과

```py
44
```

<br>

### ⌨️ 문제 풀이

1.  우선순위 큐의 성질을 이용해 각 정보의 가치를 우선순위로 정해 데이터를 관리하며 구현하는 문제이다.
2.  dictionary 로 정보의 이름을 관리하면 편하게 구현할 수 있다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
import heapq

dictionary, res = {}, 0
for _ in range(int(stdin.readline())):
    data = list(stdin.readline().split())

    info = data[:3]
    if info[0] == '1':
        try:
            for i in range(int(info[2])):
                heapq.heappush(dictionary[info[1]], (-int(data[3 + i]), int(data[3 + i])))
        except:
            dictionary[info[1]] = []
            for i in range(int(info[2])):
                heapq.heappush(dictionary[info[1]], (-int(data[3 + i]), int(data[3 + i])))

    else:
        try:
            for i in range(int(info[2])):
                res += heapq.heappop(dictionary[info[1]])[1]
        except:
            pass

print(res)
```
