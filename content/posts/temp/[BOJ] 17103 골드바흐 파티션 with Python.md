---
author: ["Jxun-h"]
title: "[BOJ] 17103 골드바흐 파티션 with Python"
date: "2022-07-06
"
description: ""
summary: ""
tags: ["자료구조", "PS", "정수론", "소수판별", "에라토스테네스의 체", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/17103" target="_blank">BOJ 17103 골드바흐 파티션</a>

<br>

### 💡 조건

1.  골드바흐의 추측: 2보다 큰 짝수는 두 소수의 합으로 나타낼 수 있다.

2.  짝수 N을 두 소수의 합으로 나타내는 표현을 골드바흐 파티션이라고 한다.  
    짝수 N이 주어졌을 때, 골드바흐 파티션의 개수를 구해보자. 두 소수의 순서만 다른 것은 같은 파티션이다.

3.  첫째 줄에 테스트 케이스의 개수 T (1 ≤ T ≤ 100)가 주어진다.  
    각 테스트 케이스는 한 줄로 이루어져 있고, 정수 N은 짝수이고, 2 < N ≤ 1,000,000을 만족한다.

4.  **정수론, 소수판별, 에라토스테네스의 체** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5
6
8
10
12
100
```

#### 실행결과

```py
1
1
2
1
6
```

<br>

### ⌨️ 문제 풀이

1.  소수판별 리스트를 만들어 반환하는 함수를 통해서 소수 리스트를 얻는다.

2.  각 테스트 케이스마다 입력받은 숫자 num // 2 + 1에 해당하는 숫자까지 순회하면서 골드바흐 파티션의 수를 세어 출력한다

<br>

### 🖥 소스 코드

```py
from sys import stdin


def prime_list(n):
    sieve = [False, False] + [True] * n
    m = int(n ** 0.5)
    for i in range(2, m + 1):
        if sieve[i]:
            for j in range(i + i, n, i):
                sieve[j] = False

    return sieve


prime_nums = prime_list(10 ** 6)

for _ in range(int(stdin.readline())):
    cnt = 0
    num = int(stdin.readline())
    for i in range((num // 2) + 1):
        if prime_nums[i] and prime_nums[num - i]:
            cnt += 1

    print(cnt)
```
