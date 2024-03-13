---
author: ["Jxun-h"]
title: "[BOJ] 5988 홀수일까 짝수일까 with Python"
date: "2023-04-03 15:52:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/5988" target="_blank">BOJ 5988 홀수일까 짝수일까</a>

<br>

### 💡 조건

1.  N개의 정수가 주어지면 홀수인지 짝수인지를 출력하는 프로그램을 작성하는 문제.
2.  N(1 <= N <= 100)
3.  N+1번째 줄에 걸쳐 홀수인지 짝수인지 확인할 정수 K (1 <= K <= 10^60)가 주어진다.
4.  N개의 줄에 걸쳐 한 줄씩 정수 K가 홀수라면 'odd'를, 짝수라면 'even'을 출력한다.
5.  **수학** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
2
1024
5931
```

#### 실행결과 1

```py
even
odd
```

<br>

### ⌨️ 문제 풀이

1.  각 숫자를 2로 나누어 나온 나머지가 0이면 even, 아니면 odd를 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

for _ in range(int(stdin.readline())):
    if int(stdin.readline()) % 2 == 0:
        print('even')
    else:
        print('odd')
```