---
author: ["Jxun-h"]
title: "[BOJ] 3273 두 수의 합 with Python"
date: "2021-08-30"
description: ""
summary: ""
tags: ["정렬", "PS", "이분탐색", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/3273" target="_blank">BOJ 3273 두 수의 합</a>

<br>

### 💡 조건 및 풀이

1.  `n`개의 서로 다른 정수로 이루어진 수열 `A`가 있다. `1 <= A[i] <= 1000000`
2.  `n`의 크기는 `1 <= n <= 100000` x의 크기는 `1 <= x <= 2000000`
3.  **sort + binary search 유형의 문제**
4.  자연수 x가 주어졌을 때, `A[i] + A[j] = x` 를 만족하는 쌍의 수를 구한다.  
    `(A[i], A[j])`

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
9
5 12 7 10 9 1 2 3 11
13
```

#### 실행결과

```python
3
```

<br>

### ⌨️ 문제 풀이

1.  `Python` 언어의 배열 이진 분할 알고리즘을 사용할 수 있는 `bisect` 사용.
2.  list로 받은 수열을 `sort()`로 정렬.
3.  정렬된 리스트에 대해 0번 인덱스부터 순차적으로 접근하며  
    `bisect_left`, `bisect_right` 함수를 사용해 반환받은 값`(l, r)`을 비교한다.
4.  수열의 총 개수(`n`)보다 `bisect_left` 로 반환받은 값(`l`)이 작을 때만 실행한다.
5.  현재 수열의 i번째 숫자와 수열의 l번째 숫자가 같지 않으며, `r`과 `l`이 같지 않을 때 `cnt += 1`
6.  따로 `for`문의 범위를 지정해주지 않으면, 정답에 해당하는 `(A[i], A[j])` 쌍이  
    두번이 나오기 때문에 `cnt // 2`를 해준다.

<br>

### 🖥 소스 코드

```python
from sys import stdin
from bisect import bisect_right, bisect_left

n = int(stdin.readline())
arr = list(map(int, stdin.readline().split()))
arr.sort()
x = int(stdin.readline())

cnt = 0

for i in range(n):
    l, r = bisect_left(arr, x - arr[i]), bisect_right(arr, x - arr[i])
    if l < n:
        if arr[i] != arr[l] and l != r:
            cnt += 1

print(cnt // 2)
```

<br>

### 💾 느낀점

- `n`을 순차적으로 접근할 `for`문의 범위를 잘못 지정해주어서 틀렸었다.
- `bisect` 라이브러리를 사용해 찾으려고 하는 **숫자의 인덱스 번호를 잘못 계산**해서 틀렸었다.
- 이분탐색 문제를 더 많이 풀어보고, 다양한 유형을 경험해보아야겠다.
