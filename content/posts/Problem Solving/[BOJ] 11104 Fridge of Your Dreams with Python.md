---
author: ["Jxun-h"]
title: "[BOJ] 11104 Fridge of Your Dreams with Python"
date: "2022-03-22"
description: ""
summary: ""
tags: ["자료구조", "PS", "진수변환", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/11104" target="_blank">BOJ 11104 Fridge of Your Dreams</a>

<br>

### 💡 조건

1.  2진수를 읽어 10진수로 출력하는 문제
2.  **진수변환** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5
000000000000000000000001
000000000001010101010101
000000000000000000001010
101011001010101100101101
111111111111111111111111
```

#### 실행결과

```py
1
5461
10
11316013
16777215
```

<br>

### ⌨️ 문제 풀이

1.  int() 함수를 사용해 2진수를 10진수로 출력해준다.
2.  int(문자열, 진수) 로 사용하면 된다

<br>

### 🖥 소스 코드

```py
from sys import stdin

for _ in range(int(stdin.readline())):
    print(int(stdin.readline().rstrip(), 2))
```

<br>

### 💾 느낀점