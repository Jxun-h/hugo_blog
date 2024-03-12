---
author: ["Jxun-h"]
title: "[BOJ] 1788 피보나치수의 확장 with Python"
date: "2022-03-06"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1788" target="_blank">BOJ 1788 피보나치수의 확장</a>

<br>

### 💡 조건

1.  피보나치 수 F(n)을 n이 음수인 경우로도 확장시킬 수 있다.
2.  F(n) = F(n-1) + F(n-2)를 n ≤ 1일 때도 성립되도록 정의하는 것이다.
3.  n = 1일 때 F(1) = F(0) + F(-1)이 성립되어야 하므로, F(-1)은 1이 되어야 한다.
4.  n이 주어졌을 때, 피보나치 수 F(n)을 구하는 프로그램을 작성하는 프로그램.  
    n은 음수로 주어질 수도 있다.
5.  n은 절댓값이 1,000,000을 넘지 않는 정수이다.  
    첫째 줄에 F(n)이 양수이면 1, 0이면 0, 음수이면 -1을 출력한다.  
    둘째 줄에는 F(n)의 절댓값을 출력한다.  
    이 수가 충분히 커질 수 있으므로, 절댓값을 1,000,000,000으로 나눈 나머지를 출력한다.
6.  **다이나믹프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
10
```

#### 실행결과

```py
1
55
```

<br>

### ⌨️ 문제 풀이

1.  피보나치 값을 저장할 fibo 리스트 크기를 150만 개로 만들어준다.  
    리스트의 첫번째 값과 두번째 값을 0 과 1로 저장한다.
2.  n 이 0보다 작은 경우, -1부터 n까지 -1씩 줄여가면서 순회한다.  
    fibo[i + 2] - fibo[i + 1] 의 점화식을 통한 값이 0 보다 작을 경우  
    fibo[i]의 값은 fibo[i + 2] - fibo[i + 1] 를 절대값 처리해 준 후, 1000000000로 나누고 다시 음수로 만들어준다.
3.  fibo[n] < 0 일 경우, -1 을 출력하고, fibo[n]를 음수로 변환하여 출력한다.
4.  fibo[n] >= 0 일 경우, 1 을 출력하고, fibo[n]을 출력한다.
5.  n > 0 경우, 일반 피보나치처럼 수를 구한다.
6.  n = 0 경우, 0을 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

fibo = [0 for _ in range(1500000)]
n = int(stdin.readline())
fibo[0:1] = [0, 1]

if n < 0:
    for i in range(-1, n - 1, -1):
        data = fibo[i+2] - fibo[i+1]
        if data < 0:
            fibo[i] = (abs(data) % 1000000000) * -1
        else:
            fibo[i] = data % 1000000000
    if fibo[n] < 0:
        print(-1)
        print(fibo[n] * -1)
    else:
        print(1)
        print(fibo[n])


elif n > 0:
    for i in range(2, n + 1):
        fibo[i] = (fibo[i - 1] + fibo[i - 2]) % 1000000000

    print(1)
    print(fibo[n])

else:
    print(0)
    print(0)
```

<br>

### 💾 느낀점

1.  음수로 피보나치를 확장하는 것이 생각보다 조금 까다로운 느낌이 있었습니다.