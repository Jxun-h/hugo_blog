---
author: ["Jxun-h"]
title: "[BOJ] 10819 차이를 최대로 with Python"
date: "2022-01-11"
description: ""
summary: ""
tags: ["자료구조", "PS", "백트래킹", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/10819" target="_blank">BOJ 10819 차이를 최대로</a>

<br>

### 💡 조건

1.  N개의 정수로 이루어진 배열 A
2.  `N (3 ≤ N ≤ 8)`
3.  배열에 들어있는 정수는 `-100보다 크거나 같고, 100보다 작거나 같다.`
4.  다음 식의 최댓값을 구하는 프로그램을 작성.
    ```py
    |A[0] - A[1]| + |A[1] - A[2]| + ... + |A[N-2] - A[N-1]|
    ```
5. **브루트포스 알고리즘 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제
```py
6  
20 1 15 8 4 10
```

#### 실행결과
```py
62
```

<br>

### ⌨️ 문제 풀이

1.  최댓값을 저장할 res 정수 생성
2.  itertools 의 permutaions 함수로 가능한 수를 모두 계산하여 v에 저장하고, res 갱신

<br>

### 🖥 소스 코드
```py
from sys import stdin  
from itertools import permutations

n = int(stdin.readline())  
arr = list(map(int, stdin.readline().split()))  
res = -int(1e9)

for arr2 in permutations(arr, n):  
v = 0  
for i in range(n-1):  
v += abs(arr2[i] - arr2[i + 1])

res = max(res, v)

print(res)
```

<br>

### 💾 느낀점

1.  배열의 크기가 최대 8개 밖에 안되기에 permutaions를 썼다.
2.  만약 배열의 크기가 컸다면?