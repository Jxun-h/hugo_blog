---
author: ["Jxun-h"]
title: "[BOJ] 9742 순열 with Python"
date: "2022-03-03"
description: ""
summary: ""
tags: ["자료구조", "PS", "백트래킹", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/9742" target="_blank">BOJ 9742 순열</a>

<br>

### 💡 조건

1.  집합의 순열이란 집합의 서로 다른 원소를 모두 사용해 만들 수 있는 순서이다.
2.  서로 다른 숫자와 문자로 이루어진 집합과 위치가 주어졌을 때, 그 집합의 순열 중 주어진 위치의 순열을 구하는 프로그램을 작성하는 문제
3.  입력은 여러 개의 테스트 케이스로 이루어져 있다. 각 테스트 케이스는 한 줄로 이루어져 있다.
4.  첫 번째 문자열은 서로 다른 숫자와 알파벳으로 이루어져 있으며, 길이는 최대 10이다.
5.  사전순 순서대로 주어진다. 문자열 다음에는 찾아야 하는 위치가 주어지며, 이 값은 3,628,800보다 작거나 같은 자연수이다.
6.  **백트래킹** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
235 4
bein 20
123456 700
mnpqr 130
tuvwxyz 4000
```

#### 실행결과

```py
235 4 = 352
bein 20 = nbie
123456 700 = 651342
mnpqr 130 = No permutation
tuvwxyz 4000 = ywuxvzt
```

<br>

### ⌨️ 문제 풀이

1.  입력받은 순열 집합의 길이의 제곱이 구하고자하는 순서의 숫자보다 작을 경우, No permutation 을 출력하면 됩니다.
2.  (1)번에 해당하지 않을 경우, 재귀호출을 통해 순열을 구하면 됩니다.
3.  테스트 케이스가 여러 개이기 때문에 while 문으로 감싼 뒤, 입력받은 문자가 2개로 나누어지지 않을 경우 break 를 해주면 됩니다.
4.  재귀호출에서 cnt 의 개수가 재귀 호출을 통해 만들어진 순열의 개수와 같아지면 그대로 문자열을 반환시키면 됩니다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from math import factorial


def solve(string, i):
    global cnt
    if i == len(a):
        cnt += 1
        if cnt == b:
            return string
    else:
        for k in a:
            if k not in string:
                res = solve(string + k, i + 1)
                if res:
                    return res

    return


while 1:
    cnt = 0
    input_data = stdin.readline().rstrip().split()

    if len(input_data) != 2:
        break

    a, b = input_data
    b = int(b)

    if factorial(len(a)) < b:
        print(a, b, '=', 'No permutation')
    else:
        print(a, b, '=', solve('', 0))
```

<br>

### 💾 느낀점

1.  입력 받은 순열 집합의 길이의 제곱이 구하고자하는 n번째, 즉 n보다 작을 경우 DFS를 돌리지 않아도 되는 사실을 몰랐다
2.  (1)번을 잘 몰랐기에 당연히 시간초과가 떠서 고생을 했던 문제이다.