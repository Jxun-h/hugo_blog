---
author: ["Jxun-h"]
title: "[BOJ] 1940 주몽 with Python"
date: "2022-02-07"
description: ""
summary: ""
tags: ["자료구조", "PS", "정렬", "투포인터", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1940" target="_blank">BOJ 1940 주몽</a>

<br>

### 💡 조건

1.  갑옷은 두 개의 재료로 만드는데 두 재료의 고유한 번호를 합쳐서 M(1 ≤ M ≤ 10,000,000)이 되면 갑옷이 만들어 지게 된다.
2.  N(1 ≤ N ≤ 15,000) 개의 재료와 M이 주어졌을 때 몇 개의 갑옷을 만들 수 있는지를 구하는 문제
3.  **정렬, 투 포인터** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
6
9
2 7 4 1 5 3
```

#### 실행결과

```py
2
```

<br>

### ⌨️ 문제 풀이

1.  정렬을 해서 투포인터를 사용해 문제를 푸는 것이 이 문제의 요점인 것 같다.
2.  나는 파이썬 bisect 라이브러리의 bisect\_left 를 써서 쉽게 풀수 있었다.
3.  재료들의 각 고유번호를 입력받아 놓은 arr이라는 변수를 정렬하고 순회한다.
4.  (3)번을 통해 순회하는 값인 i가 있다.  
    갑옷이 만들어지기 위한 값 m 에서 i를 뺀 값이 arr 리스트에 위치하고 있는지  
    bisect\_left 를 통해 이분탐색해준 결과를 f 변수에 저장한다.  
    f 가 n 보다 작고, arr\[f\]가 i와 같지 않다면, i + f는 m이다.
5.  (4)에서 나온 결과 값이 참인지 확인하고, (arr\[f\], i) 의 쌍이 한번도 나온적 없는 조합이라면  
    res + 1을 해주고, (arr\[f\], i), (i, arr\[f\]) 를 visited에 저장해 이미 나온 조합이라고 표시해둔다.
6.  (1)~(5) 과정을 거치고 난 후, res를 출력해준다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from bisect import bisect_left

n = int(stdin.readline())
m = int(stdin.readline())
arr = sorted(list(map(int, stdin.readline().split())))
res = 0
visited = set()
arr.sort()

for i in arr:
    f = bisect_left(arr, m-i)
    if f < n and arr[f] != i:
        temp = arr[f]
        if temp + i == m and (temp, i) not in visited:
            visited.add((temp, i))
            visited.add((i, temp))
            res += 1

print(res)
```

<br>

### 💾 느낀점

1.  투포인터로 풀면 훨씬 쉬웠을 것 같은데, 3달 전의 나는 왜 bisect 라이브러리를 사용했을까?
2.  투포인터를 연습하기 매우 좋은 문제인 것 같다.