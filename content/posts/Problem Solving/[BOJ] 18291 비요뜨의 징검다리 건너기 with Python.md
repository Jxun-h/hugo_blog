---
author: ["Jxun-h"]
title: "[BOJ] 18291 비요뜨의 징검다리 건너기 with Python"
date: "2022-05-20"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/18291" target="_blank">BOJ 18291 비요뜨의 징검다리 건너기</a>

<br>

### 💡 조건

1.  징검다리는 비요뜨가 있는 방향에서부터 반대 방향까지 차례로 1번, 2번, ..., N번의 번호를 가지고 있다.

2.  비요뜨는 1번 징검다리 위에 올라갔다. 그리고 아래 두 가지 규칙을 지키며 징검다리를 건너려고 한다.
    1.  1 ≤ X ≤ N 인 임의의 정수 X에 대해, 현재 있는 징검다리의 번호를 i번이라고 할 때 i+X번 징검다리로 뛸 수 있다.
    2.  N번째 징검다리를 지나쳐선 안 되고, 정확히 도착해야 한다

3.  첫 번째 줄에 테스트 케이스의 수 T가 주어진다. (1 ≤ T ≤ 1000)

4.  각 테스트 케이스는 한 줄로 구성되며, 징검다리의 개수를 의미하는 N이 주어진다. (1 ≤ N ≤ 109)

5.  각 테스트 케이스에 대해, 한 줄에 하나씩 규칙을 만족하면서 **징검다리를 건너는 경우의 수**를 109+7로 나눈 나머지를 출력한다.

6.  **수학** 유형의 문제


<br>

## 🔖 예제 및 실행결과

#### 예제

```py
1
4
```

#### 실행결과

```py
4
```

<br>

## ⌨️ 문제 풀이

1.  분할정복을 통한 거듭제곱 문제이다. 재귀를 사용하지 않고 문제를 해결했다.

2.  pow 를 사용할 경우 시간초과가 뜬다.

<br>

## 🖥 소스 코드

```py
from sys import stdin


def solve(x):
    mod = 1000000007
    a = 2
    b = x
    ret = 1
    while b:
        if b % 2 == 1:
            ret *= a
            ret %= mod

        a *= a
        a %= mod
        b //= 2

    return ret


for _ in range(int(stdin.readline())):
    test_data = int(stdin.readline())
    if 0 < test_data < 2:
        print(1)

    else:
        x = test_data - 2
        print(solve(x))
```