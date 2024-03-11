---
author: ["Jxun-h"]
title: "[BOJ] 18511 큰 수 구성하기 with Python"
date: "2021-12-18"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "브루트포스", "알고리즘", "재귀", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/18511" target="_blank">BOJ 18511 큰 수 구성하기</a>

<br>

### 💡 조건

1.  `N`보다 작거나 같은 자연수 중에서, 집합 `K`의 원소로만 구성된 가장 큰 수를 출력하는 프로그램을 작성.  
    `(10 ≤ N ≤ 100,000,000, 1 ≤ K의 원소의 개수 ≤ 3)`
2.  `K`의 모든 원소는 `1부터 9까지의 자연수`로만 구성된다.
3.  첫째 줄에 `N보다 작거나 같은 자연수` 중에서, `K의 원소로만 구성된 가장 큰 수`를 출력
4.  **브루트포스 알고리즘, 재귀함수 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
657 3
1 5 7
```

#### 실행결과

```py
577
```

<br>

### ⌨️ 문제 풀이

1.  `n`을 문자열로 바꾸었을 때의 길이를 `le` 라는 변수에 저장한다.
2.  `n`보다 같거나 작은 자연수 중에 주어진 수열 `arr`로 만들 수 있는  
    최댓값을 만들기 위해서 `solve()` 함수 안에서 수행해야할 로직은 다음과 같다.
    -   1.  `itertools`의 `product()` 함수를 사용하여 수열 `arr`로 만들 있는 모든 경우의 `k`자리의 수를 모두 구해 변수 `temp`에 저장한다.
    -   2.  `temp`의 원소들을 하나씩 순회하면서, 각 원소에 해당하는 `t`가 `n`보다 작거나 같은지 확인한다
    -   3.  위의 조건이 만족될 경우, 결과값 `res`보다 `t`가 클 경우 `res`를 갱신한다.
    -   4.  만약 `temp`를 모두 순회했지만 `res`가 갱신이 안되어 `-int(1e9)` 일 경우, `le - 1`  
            갱신이 되었다면 `res`반환하고 출력

<br>

### 🖥 소스 코드

```py
from sys import stdin
from itertools import product

n, k = map(str, stdin.readline().split())
arr = list(map(int, stdin.readline().split()))
arr.sort(reverse=True)
le = len(n)
res = -int(1e9)


def solve(le):
    global res

    while 1:
        temp = list(product(arr, repeat=le))
        for i in temp:
            t = int(''.join(map(str, i)))
            if int(t) <= int(n):
                res = max(res, t)

        if res == -int(1e9):
            le -= 1
        else:
            return res


solve(le)
print(res)
```

<br>

### 💾 느낀점

1.  `temp`를 모두 순회했을 때 `res`가 갱신이 안된 경우를 처리하지 못해 골치아팠다.