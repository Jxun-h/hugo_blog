---
author: ["Jxun-h"]
title: "[BOJ] 1676 팩토리얼 0의 개수 with Python"
date: "2023-04-01 22:49:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1676" target="_blank">BOJ 1676 팩토리얼 0의 개수</a>

<br>

### 💡 조건

1.  N!에서 뒤에서부터 처음 0이 아닌 숫자가 나올 때까지 0의 개수를 구하는 프로그램을 작성하는 문제.
2.  첫째 줄에 N이 주어진다. (0 ≤ N ≤ 500)
3.  **수학** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
10
```

#### 실행결과 1

```py
2
```

#### 예제 2

```py
3
```

#### 실행결과 2

```py
0
```

<br>

### ⌨️ 문제 풀이

1.  리스트에 팩토리얼 계산 값을 미리 넣어놓으면 쉽게 해결할 수 있다.
2.  N에 해당하는 값을 꺼내 맨 우측부터 좌측 방향으로 이동하며 0이 아닌 수가 나올 때까지 0의 개수가 몇 개인지 세면 된다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

arr = [1, 2, 6, 24, 120]

n = int(stdin.readline())
if n < 5:
    print(0)
else:
    for i in range(6, 501):
        arr.append(arr[-1] * i)

    ans = 0
    s = str(arr[n-1])
    for i in range(len(s)-1, -1, -1):
        if s[i] == '0':
            ans += 1
        else:
            print(ans)
            break
```