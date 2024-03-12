---
author: ["Jxun-h"]
title: "[BOJ] 10166 관중석 with Python"
date: "2022-03-16"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "정수론", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/10166" target="_blank">BOJ 10166 관중석</a>

<br>

### 💡 조건

1.  반지름이 1인 원 위에는 좌석이 1개, 반지름이 2인 원 위에는 좌석이 2개, 이런 식으로 반지름이 D 인 원 위에는 좌석이 D 개가 있다.
2.  무대에서 정확히 북쪽 방향에는 모든 원들에 좌석이 있으며, 하나의 원 위에 있는 좌석들은 동일한 간격을 두고 배치되어 있다.
3.  공연에 반지름이 D1보다 같거나 크고, D2(D1 ≤ D2)보다 같거나 작은 원들에 배치된 좌석만을 활용하려고 한다.
4.  좌석을 점으로 간주했을 때, 다른 좌석에 의해 무대 중심이 가려지는 좌석은 사용하지 않고, 그렇지 않은 좌석은 모두 사용한다.
5.  숫자는 원의 반지름을 나타내고, ●은 공연에 사용되는 좌석, ⊗은 공연에 사용되지 않는 좌석을 나타낸다.  
    원의 반지름 D1과 D2가 양의 정수로 주어진다. 단, 1 ≤ D1 ≤ D2 ≤ 2,000이다.
6.  **수학, 정수론** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3 6
```

#### 실행결과

```py
12
```

<br>

### ⌨️ 문제 풀이

1.  D1부터 D2까지 순회하면서 자리 찾기
2.  1번부터 i까지 좌석을 찾아서 최대공약수를 구하고 확인하고있는 자리들을 최대공약수 g로 나누어준다.
3.  확인하려는 자리가 이미 어딘가에 가려져 있다면 pass, 아니면 ans += 1

<br>

### 🖥 소스 코드

```py
from sys import stdin
from math import gcd


def solve():
    a, b = map(int, stdin.readline().split())
    arr = [[0] * b for _ in range(b)]

    ans = 0

    for i in range(a, b + 1):
        for j in range(1, i + 1):
            g = gcd(i, j)

            x, y = i // g, j // g

            if not arr[x-1][y-1]:
                arr[x-1][y-1] = 1
                ans += 1

    print(ans)

solve()
```

<br>

### 💾 느낀점

1.  문제를 어떻게 풀어야할지 아예 감이 오질 않아서 문제의 해설을 보고 풀었습니다.
2.  수학에 관련된 문제를 많이 어려워하는 것 같습니다.