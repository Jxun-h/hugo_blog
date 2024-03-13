---
author: ["Jxun-h"]
title: "[BOJ] 15655 N과 M (6) with Python"
date: "2023-04-18 16:33:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "백트래킹", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/15655" target="_blank">BOJ 15655 N과 M (6)</a>

<br>

### 💡 조건

1.  N개의 자연수와 자연수 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하는 문제.  
    N개의 자연수는 모두 다른 수이다.
2.  **N개의 자연수 중에서 M개를 고른 수열  
    수열은 오름차순이어야 한다.**
3.  첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)
4.  둘째 줄에 N개의 수가 주어진다. 입력으로 주어지는 수는 10,000보다 작거나 같은 자연수이다.
5.  한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다. 중복되는 수열을 여러 번 출력하면 안되며,  
    수열은 공백으로 구분해서 출력해야 한다. 수열은 사전 순으로 증가하는 순서로 출력해야 한다.
6.  **백트래킹** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
3 1
4 5 2
```

#### 실행결과 1

```py
2
4
5
```

#### 예제 2

```py
4 2
9 8 7 1
```

#### 실행결과 2

```py
1 7
1 8
1 9
7 8
7 9
8 9
```

#### 예제 3

```py
4 4
1231 1232 1233 1234
```

#### 실행결과 3

```py
1231 1232 1233 1234
```

<br>

### ⌨️ 문제 풀이

1.  입력받은 배열을 sort 함수를 통해 정렬한다.
2.  함수 f에서는 m과 cnt가 같을 때 결과값을 담고 있는 res 배열의 원소를 출력해준다.
3.  함수 f에서는 res 배열의 길이가 0보다 클 때 res 배열의 맨 마지막의 원소와 현재 넣으려고 하는 숫자를 비교해 넣는다.  
    **오름차순**

<br>

### 🖥 소스 코드

```py
from sys import stdin, setrecursionlimit

setrecursionlimit(10 ** 7)

n, m = map(int, stdin.readline().split())
arr = list(map(int, stdin.readline().split()))
arr.sort()


def f(res, cnt):
    if cnt == m:
        print(*res)
        return

    for i in range(cnt, n):
        if len(res) > 0:
            if res[-1] < arr[i]:
                f(res + [arr[i]], cnt + 1)
        else:
            f(res + [arr[i]], cnt + 1)


f([], 0)
```