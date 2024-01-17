---
author: ["Jxun-h"]
title: "[BOJ] 2143 두 배열의 합 with Python"
date: "2021-10-12"
description: ""
summary: ""
tags: ["누적합", "PS", "prefix sum", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2143" target="_blank">BOJ 2143 두 배열의 합</a>

<br>

## 💡 조건 및 풀이

1.  `(-1,000,000,000 ≤ T ≤ 1,000,000,000)`
2.  `(1 ≤ n ≤ 1,000)`
3.  `(1 ≤ m ≤ 1,000)`
4.  **누적합 유형의 문제**
5.  두 배열의 부분배열을 사용하여 합을 구해 `T`를 만들 수 있는 개수를 구한다.

<br>

## 🔖 예제 및 실행결과

#### 예제

```
5
4
1 3 1 2
3
1 3 2
```

#### 실행결과

```
7
```

<br>

## ⌨️ 문제 풀이

1.  A 부분 배열의 합들과 B 부분 배열의 합들을 더해 T가 만들어지는 경우의 수를 구하는 문제였다.
2.  두 배열을 각 구간에 해당하는 누적합을 각각의 dict 자료구조에 넣고, 중복되어 나오는 경우 +1 을 해준다.
3.  A 배열의 키 값을 순차적으로 순회하면서  
    구하고자 하는 t 값에서 A 배열의 키 값을 빼준 값이 B배열의 키값으로 있다면,  
    res에 해당 B배열의 값과 A배열의 값을 곱하여 더해준다.
    
    ```
    for key in Asum.keys():
     if (t - key) in Bsum:
         res += Bsum[t - key] * Asum[key]
    ```

<br>

## 🖥 소스 코드

```python
from sys import stdin, setrecursionlimit

setrecursionlimit(int(1e9))

t = int(stdin.readline())
n = int(stdin.readline())
A = list(map(int, stdin.readline().split()))

m = int(stdin.readline())
B = list(map(int, stdin.readline().split()))

Asum = {}
for i in range(n):
    for j in range(i, n):
        k = sum(A[i:j + 1])
        if k in Asum:
            Asum[k] += 1
        else:
            Asum[k] = 1

Bsum = {}
for i in range(m):
    for j in range(i, m):
        k = sum(B[i:j + 1])
        if k in Bsum:
            Bsum[k] += 1
        else:
            Bsum[k] = 1

res = 0

for key in Asum.keys():
    if (t - key) in Bsum:
        res += Bsum[t - key] * Asum[key]

print(res)
```

<br>

## 💾 느낀점

-   처음에 아이디어가 떠오르지않아 힘들어했다.
-   수학, DP가 제일 약한 것 같다는 생각이 들었다.
-   Dict 자료구조를 좋아하는데 이렇게 사용을 해봐서 더 좋았다.