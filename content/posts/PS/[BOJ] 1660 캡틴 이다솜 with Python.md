---
author: ["Jxun-h"]
title: "[BOJ] 1660 캡틴 이다솜 with Python"
date: "2022-03-06"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1660" target="_blank">BOJ 1660 캡틴 이다솜</a>

<br>

### 💡 조건

1.  N은 300,000보다 작거나 같은 자연수이다.
2.  사면체를 만드는 방법은 길이가 N인 정삼각형 모양을 만든다.  
    그 위에 길이가 N-1인 정삼각형 모양을 얹고 그위에 계속 해서 얹어서 1크기의 정삼각형 모양을 얹으면 된다.
3.  N개의 대포알로 만들 수 있는 사면체의 최소 개수를 출력하는 프로그램을 작성하는 문제
4.  **다이나믹프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
15
```

#### 실행결과

```py
3
```

<br>

### ⌨️ 문제 풀이

1.  대포알의 개수는 1, 4, 10, 20 ... 순으로 늘어난다.
2.  n이 30만이기 때문에 모두 한번에 다 구해놓기에는 힘들기 떄문에,  
    n보다 같거나 많은 양의 대포가 쌓여있는 사면체가 처음 등장할때까지 구해야한다.
3.  N 이 15라면 1, 4, 10 으로 만들 수 있다.  
    15는 14에서 1을 더해 만들 수 있다. 10에서 4를 더하고, 5에서 10을 더해서 만들 수 있다.
4.  dp10384 팬그램[i10384 팬그램] = min(dp10384 팬그램[i10384 팬그램], 1 + dp10384 팬그램[i - num10384 팬그램])  
    라는 점화식을 세울 수 있다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
arr = []
num = 0
i = 1

while n > num:
    num += (i * (i + 1)) // 2
    arr.append(num)
    i += 1

dp = [int(1e9) for i in range(n + 1)]
for i in range(1, n + 1):
    for num in arr:
        if num == i:
            dp[i] = 1
            break
        elif num > i:
            break
        dp[i] = min(dp[i], 1 + dp[i - num])

print(dp[n])
```

<br>

### 💾 느낀점

1.  다이나믹... 프로그래밍...