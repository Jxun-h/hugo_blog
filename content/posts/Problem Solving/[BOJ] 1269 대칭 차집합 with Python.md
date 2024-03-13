---
author: ["Jxun-h"]
title: "[BOJ] 1269 대칭 차집합 with Python"
date: "2022-03-10"
description: ""
summary: ""
tags: ["자료구조", "PS", "해시맵", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1269" target="_blank">BOJ 1269 대칭 차집합</a>

<br>

### 💡 조건

1.  자연수를 원소로 갖는 공집합이 아닌 두 집합 A와 B가 있다.
2.  두 집합 A와 B가 있을 때, (A-B)와 (B-A)의 합집합을 A와 B의 대칭 차집합이라고 한다.
3.  예를 들어, A = { 1, 2, 4 } 이고, B = { 2, 3, 4, 5, 6 } 라고 할 때,  
    A-B = { 1 } 이고, B-A = { 3, 5, 6 } 이므로,  
    대칭 차집합의 원소의 개수는 1 + 3 = 4개이다.
4.  각 집합의 원소의 개수는 200,000을 넘지 않으며, 모든 원소의 값은 100,000,000을 넘지 않는다.
5.  대칭 차집합의 원소의 개수를 출력하는 문제
6.  **해시맵, 자료구조** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3 5
1 2 4
2 3 4 5 6
```

#### 실행결과

```py
4
```

<br>

### ⌨️ 문제 풀이

1.  집합 A의 원소의 개수와 집합 B의 원소의 개수를 입력 받는다.
2.  각 집합의 원소를 set()으로 입력받아 저장한다.
3.  (a - b) 의 길이와 (b - a)의 길이를 더한 뒤 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
n, m = map(int, stdin.readline().split())
a = set(map(int, stdin.readline().split()))
b = set(map(int, stdin.readline().split()))
print(len(a - b) + len(b - a))
```

<br>

### 💾 느낀점