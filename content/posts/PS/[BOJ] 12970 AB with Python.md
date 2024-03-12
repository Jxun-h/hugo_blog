---
author: ["Jxun-h"]
title: "[BOJ] 12970 AB with Python"
date: "2022-05-09"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "그리디", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/12970" target="_blank">BOJ 12970 AB</a>

<br>

### 💡 조건

1.  문자열의 길이 n
2.  0 ≤ i < j < N 이면서 s[i] == 'A' && s[j] == 'B'를 만족하는 (i, j) 쌍의 개수 K 개가 있다.
3.  N과 K가 주어진다. (2 ≤ N ≤ 50, 0 ≤ K ≤ N(N-1)/2)
4.  문제의 조건을 만족하는 문자열 S를 출력한다. 가능한 S가 여러 가지라면, 아무거나 출력한다.
5.  S가 존재하지 않는 경우에는 -1을 출력한다.
6.  **수학, 그리디 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3 2
```

#### 실행결과

```py
ABB
```

<br>

### ⌨️ 문제 풀이

1.  문자열 s는 B로 n만큼 채워서 초기화한다.
2.  예제 4번을 예로 들면, BBBBBBBBBB 으로 먼저 s를 초기화한다.
3.  오른쪽 기준 두번째 부터 A를 넣는데, 끝에 넣어봐야 쌍의 개수가 0이기 때문에 두번째부터 넣는다.
4.  A를 왼쪽으로 밀면서 쌍의 개수를 검사한다.
5.  curk 의 값이 k가 되었을 때, while 을 종료하고, 문자열을 출력해준다.
6.  만약 while 이 종료된 후에도 curk 값이 k 의 값과 같지 않다면, 문자열을 만들 수 없는 것이니 -1을 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
n, k = map(int, stdin.readline().split())


def solve(n, k):
    s = list('B' * n)
    acnt, curk, lidx = 0, 0, -1

    while curk < k:
        if lidx <= acnt - 1:
            if s[n - 1 - (acnt + 1)] == 'A':
                break

            s[n - 1 - (acnt + 1)] = 'A'
            lidx = n - 1 - (acnt + 1)
            acnt += 1
            curk += 1
        else:
            s[lidx] = 'B'
            s[lidx - 1] = 'A'
            lidx -= 1
            curk += 1

    return s if curk == k else '-1'


answer = solve(n, k)
print(*answer, sep='')
```

<br>

### 💾 느낀점

1.  그리디는 너무 어렵다.
2.  문제가 조금 난이도가 높아지면 손을 대지 못하는 상황이 오는 것 같다.
3.  그리디 유형을 더욱 풀어봐야겠다.