---
author: ["Jxun-h"]
title: "[BOJ] 15792 A/B - 2 with Python"
date: "2023-04-10 13:03:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "수학", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/15792" target="_blank">BOJ 15792 A/B - 2</a>

<br>

### 💡 조건

1.  두 정수 A와 B를 입력받은 다음, A/B 의 값을 출력하는 문제.
2.  첫째 줄에 A와 B가 주어진다. (0 < A, B ≤ 10,000)
3.  이 문제는 서브태스크가 있다.

<center><img src='/15792.png' /></center>
<br>

4.  **구현, 수학** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
1 3
```

#### 실행결과 1

```py
0.33333333333333333333333333333333
```

#### 예제 2

```py
4 5
```

#### 실행결과 2

```py
0.8
```

<br>

### ⌨️ 문제 풀이

1.  해당 문제의 서브태스크 10번을 보면, 절대/상대 오차 허용 범위가 10**-1000 이다.
2.  이는 소수점 1000자리까지의 수의 오차범위를 허용해준다는 것이니, 이를 생각하고 구현을 하면된다.
3.  실수에는 정수부와 소수부가 있다. 이를 따로 나누어 계산을 해주고 문자열로 붙여서 출력하면 편하다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
a, b = map(int, stdin.readline().split())
ans = '' + str(a // b) + '.'
a %= b
a *= 10

for _ in range(1000):
    temp = a // b
    ans += str(temp)
    a %= b
    a *= 10

print(ans)
```