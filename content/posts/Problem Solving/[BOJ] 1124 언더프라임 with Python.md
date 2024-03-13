---
author: ["Jxun-h"]
title: "[BOJ] 1124 언더프라임 with Python"
date: "2023-04-11 15:20:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "소수판정", "에라토스테네스의 체", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1124" target="_blank">BOJ 1124 언더프라임</a>

<br>

### 💡 조건

1.  자연수 X를 소인수분해하면, 곱해서 X가 되는 소수의 목록을 얻을 수 있다.  
    예를 들어, 12 = 2 × 2 × 3이다. 1은 소수가 아니다.
2.  어떤 수 X를 소인수분해 해서 구한 소수의 목록의 길이가 소수이면, 그 수를 언더프라임 이라고 한다.
3.  12는 목록에 포함된 소수의 개수가 3개이고, 3은 소수이니 12는 언더프라임이다.
4.  두 정수 A와 B가 주어졌을 때, A보다 크거나 같고, B보다 작거나 같은 정수 중에서 언더프라임인 것의 개수를 구하는 문제
5.  2 ≤ A ≤ B ≤ 100,000
6.  **에라토스테네스의 체, 수학, 소수판정** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
2 10
```

#### 실행결과 1

```py
5
```

#### 예제 2

```py
100 105
```

#### 실행결과 2

```py
2
```

#### 예제 3

```py
17 17
```

#### 실행결과 3

```py
0
```

#### 예제 4

```py
123 456
```

#### 실행결과 4

```py
217
```

<br>

### ⌨️ 문제 풀이

1.  에라토스테네스의 체를 이용해 소수를 판단할 수 있는 is_prime 리스트와 판정된 소수를 담을 primes 리스트를 만든다.
2.  0과 1은 소수가 아니기에, is_prime 리스트에서 반드시 0 값을 넣어줘야 한다.
3.  A 부터 B 까지의 범위를 순회하면서, 만들어 놓은 primes 배열도 순회한다.  
    A 부터 B 까지의 범위의 숫자를 primes 배열의 숫자로 나누면서 1을 제외한 소수의 개수를 센다.
4.  (3)에서 나온 숫자가 is_prime에서 소수로 판별이 된다면 res += 1
5.  A 부터 B 까지 순회가 끝났다면, res 를 반환한 후 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

a, b = map(int, stdin.readline().split())
is_prime = [1 for i in range(100001)]
primes = []
is_prime[0:1] = 0, 0


def prime_checker():
    for i in range(2, 100000):
        if is_prime[i] == 1:
            primes.append(i)
            temp, length = i + i, len(is_prime)
            while length > temp:
                is_prime[temp] = 0
                temp += i


def check_under_prime(a, b):
    prime_checker()

    res = 0
    for i in range(a, b + 1):
        cnt, idx = 0, 0
        while 1:
            if i % primes[idx] == 0:
                cnt += 1
                i //= primes[idx]

                if i == 1:
                    break
            else:
                idx += 1
        if is_prime[cnt] == 1:
            res += 1

    return res


print(check_under_prime(a, b))
```