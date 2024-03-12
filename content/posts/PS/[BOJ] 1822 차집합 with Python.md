---
author: ["Jxun-h"]
title: "[BOJ] 1822 차집합 with Python"
date: "2022-03-06"
description: ""
summary: ""
tags: ["자료구조", "PS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1822" target="_blank">BOJ 1822 차집합</a>

<br>

### 💡 조건

1.  집합 A에는 속하면서 집합 B에는 속하지 않는 모든 원소를 구하는 프로그램을 작성하는 문제.
2.  집합 A의 원소의 개수 n(A)와 집합 B의 원소의 개수 n(B)가 빈 칸을 사이에 두고 주어진다.
3.  (1 ≤ n(A), n(B) ≤ 500,000)이 주어진다.
4.  둘째 줄에는 집합 A의 원소가, 셋째 줄에는 집합 B의 원소가 빈 칸을 사이에 두고 주어진다.
5.  하나의 집합의 원소는 2,147,483,647 이하의 자연수이며, 하나의 집합에 속하는 모든 원소의 값은 다르다.
6.  **지료구조** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4 3
2 5 11 7
9 7 4
```

#### 실행결과

```py
3
2 5 11
```

<br>

### ⌨️ 문제 풀이

1.  각 집합의 원소의 개수를 입력받는다.
2.  각 집합을 입력받되, set() 자료구조에 입력을 받는다.
3.  a 집합 자료형에서 b 집합 자료형을 빼준 결과값을 res에 저장한다.
4.  res가 빈 값이라면, 0을 출력한다.
5.  res가 비어있지 않다면, res의 길이와 정렬된 res를 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = map(int, stdin.readline().split())
a = set(map(int, stdin.readline().split()))
b = set(map(int, stdin.readline().split()))

res = a-b

if res:
    print(len(res))
    print(*sorted(list(res)))
else:
    print(0)
```

<br>

### 💾 느낀점

1.  해시맵 자료구조를 사용한 간단한 문제였습니다.