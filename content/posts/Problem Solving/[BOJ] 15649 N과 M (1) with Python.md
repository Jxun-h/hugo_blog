---
author: ["Jxun-h"]
title: "[BOJ] 15649 N과 M (1) with Python"
date: "2023-04-18 15:36:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "백트래킹", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/15649" target="_blank">BOJ 15649 N과 M (1)</a>

<br>

### 💡 조건

1.  자연수 N과 M이 주어졌을 때, 아래 조건을 만족하는 길이가 M인 수열을 모두 구하는 프로그램을 작성하는 문제
2.  **1부터 N까지 자연수 중에서 중복 없이 M개를 고른 수열**
3.  첫째 줄에 자연수 N과 M이 주어진다. (1 ≤ M ≤ N ≤ 8)
4.  한 줄에 하나씩 문제의 조건을 만족하는 수열을 출력한다.
5.  중복되는 수열을 여러 번 출력하면 안되며, 각 수열은 공백으로 구분해서 출력해야 한다.  
    수열은 사전 순으로 증가하는 순서로 출력해야 한다.
6.  **백트래킹** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
3 1
```

#### 실행결과 1

```py
1
2
3
```

#### 예제 2

```py
4 2
```

#### 실행결과 2

```py
1 2
1 3
1 4
2 1
2 3
2 4
3 1
3 2
3 4
4 1
4 2
4 3
```

#### 예제 3

```py
4 4
```

#### 실행결과 3

```py
1 2 3 4
1 2 4 3
1 3 2 4
1 3 4 2
1 4 2 3
1 4 3 2
2 1 3 4
2 1 4 3
2 3 1 4
2 3 4 1
2 4 1 3
2 4 3 1
3 1 2 4
3 1 4 2
3 2 1 4
3 2 4 1
3 4 1 2
3 4 2 1
4 1 2 3
4 1 3 2
4 2 1 3
4 2 3 1
4 3 1 2
4 3 2 1
```

<br>

### ⌨️ 문제 풀이

1.  1부터 N 까지 자연수 중에서 중복없이 M 개를 고르는 법은 itertools 라이브러리 내의 permutations 함수를 사용하면 된다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from itertools import permutations

n, m = map(int, stdin.readline().split())
for per in list(permutations([i for i in range(1, n + 1)], m)):
    print(*per)
```