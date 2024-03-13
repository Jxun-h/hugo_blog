---
author: ["Jxun-h"]
title: "[BOJ] 1789 수들의 합 with Python"
date: "2023-04-03 16:26:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "그리디", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1789" target="_blank">BOJ 1789 수들의 합</a>

<br>

### 💡 조건

1.  서로 다른 N개의 자연수의 합이 S라고 한다. S를 알 때, 자연수 N의 최댓값은 얼마일까?
2.  첫째 줄에 자연수 S(1 ≤ S ≤ 4,294,967,295)가 주어진다.
3.  첫째 줄에 자연수 N의 최댓값을 출력한다.
4.  **수학, 그리디 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
200
```

#### 실행결과 1

```py
19
```

<br>

### ⌨️ 문제 풀이

1.  계산하고 있는 계산값(A), 정답(B), 더할 수(C)를 각각 변수로 만든다.
2.  while를 이용해 반복적인 계산을 한다.  
    A += C 후, C += 1, B += 1
3.  (2)번의 반복문은 A가 입력 받은 S 보다 작을때만 반복한다.
4.  while 의 조건에 해당되지 않아 반복문이 종료되었으면 조건에 맞게 출력한다.
5.  만약 A가 S와 값이 같다면 ans를, 그게 아니라면 ans -1 을 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

s = int(stdin.readline())
ans, res, num = 0, 0, 1

while res < s:
    res += num
    num += 1
    ans += 1

print(ans if res == s else ans - 1)
```