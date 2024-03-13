---
author: ["Jxun-h"]
title: "[BOJ] 1038 감소하는 수 with Python"
date: "2022-03-23"
description: ""
summary: ""
tags: ["자료구조", "PS", "백트래킹", "브루트포스", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1038" target="_blank">BOJ 1038 감소하는 수</a>

<br>

### 💡 조건

1.  음이 아닌 정수 X의 자릿수가 가장 큰 자릿수부터 작은 자릿수까지 감소한다면, 그 수를 감소하는 수라고 한다.
2.  N번째 감소하는 수를 출력하는 문제.
3.  0은 0번째 감소하는 수이고, 1은 1번째 감소하는 수이다. 만약 N번째 감소하는 수가 없다면 -1을 출력한다.
4.  N은 1,000,000보다 작거나 같은 자연수 또는 0이다.
5.  **백트래킹, 브루트포스** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
18
```

#### 실행결과

```py
42
```

<br>

### ⌨️ 문제 풀이

1.  줄어드는 수를 구해서 dp 리스트에 이어붙여준다.
2.  0에서 9까지는 미리 dp 생성 할 때 넣어둔 후, 재귀함수를 호출해 줄어드는 수를 구해 넣어준다.
3.  dp 리스트를 정렬해준 뒤, n이 리스트의 범위를 초과한다면 -1을 출력해준다.
4.  초과하지 않는다면 dp[n] 을 출력한다.
5.  숫자를 순회하면서 하는 것이 아닌, 문자를 이어붙이면서 줄어드는 수를 만들면서 구하면 쉽게 구할 수 있다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

dp = [x for x in range(10)]


def solve(cnt, s, num):
    if cnt == len(s):
        dp.append(int(s))
        return

    for i in range(num, -1, -1):
        if not s:
            solve(cnt, s + str(i), num - 1)
        else:
            if int(s[-1]) > i:
                solve(cnt, s + str(i), i - 1)


for i in range(2, 11):
    solve(i, '', 9)

dp.sort()
n = int(stdin.readline())
if len(dp) - 1 < n:
    print(-1)
else:
    print(dp[n])
```

<br>

### 💾 느낀점

1.  조금 헤맬뻔 했지만 바로 정답을 맞출 수 있는, 티어에 비해 별로 어렵지 않은 문제였다.