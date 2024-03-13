---
author: ["Jxun-h"]
title: "[BOJ] 5568 카드 놓기 with Python"
date: "2021-08-31"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/5568" target="_blank">BOJ 5568 카드 놓기</a>

<br>

### 💡 조건 및 풀이

1.  카드의 장수는 `4 <= N <= 10`
2.  각 카드에 숫자가 적혀있다. `1 <= 숫자 <= 99`
3.  `N`개의 카드 중에서 `K`개의 카드를 골라서 몇 가지 수를 만들 수 있을까?
4.  **브루트포스 유형의 문제**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
6
3
72
2
12
7
2
1
```

#### 실행결과

```python
68
```

<br>

### ⌨️ 문제 풀이

1.  `from itertools import permutaions`  
    permutations라는 순열 함수를 사용했다.  
    리스트와 값을 넣으면 리스트에서 그만큼의 개수대로 숫자를 꺼낸다.
2.  리스트에는 같은 숫자도 존재하며, 충분히 순열로 리스트를 만들었을 때, 중복이 존재한다.
3.  결과를 반환할 set() 자료구조를 만든 후
4.  for 문을 사용해서 순열리스트에 차례대로 접근하면서, 문자열로 만들어주면서 합친다.
5.  합쳐진 문자열을 set() 자료구조로 만든 변수에 추가한다.
    -   **중복으로 추가가 되지 않는다**
6.  set() 변수의 길이를 재서 출력.

<br>

### 🖥 소스 코드

```python
from sys import stdin
from itertools import permutations as p

arr = []
n, k = int(stdin.readline()), int(stdin.readline())
for i in range(n):
    arr.append(int(stdin.readline()))

res = set()
for i in list(p(arr, k)):
    res.add(''.join(list(map(str, i))))

print(len(res))
```

<br>

### 💾 느낀점

-   처음엔, 순열 리스트로만 만들어서 길이를 쟀다. -> TLE
-   순열 리스트에 순차적으로 접근해서 문자열로 만들어 조합을 본 뒤  
    풀어나가는 아이디어, set() 자료구조를 사용할 아이디어를 떠올린 뒤  
    바로 풀었다.
-   비교적 실버 문제가 쉽고 개념을 쌓기에 좋은 문제들이 많은 것 같다.