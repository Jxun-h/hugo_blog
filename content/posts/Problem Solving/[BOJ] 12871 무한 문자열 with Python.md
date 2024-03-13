---
author: ["Jxun-h"]
title: "[BOJ] 12871 무한 문자열 with Python"
date: "2023-04-13 11:42:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "문자열", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/12871" target="_blank">BOJ 12871 무한 문자열</a>

<br>

### 💡 조건

1.  문자열 s가 있을 때, f(s)는 s를 무한번 붙인 문자열로 정의한다.  
    예를 들어, s = "abc" 인 경우에 f(s) = "abcabcabcabc..."가 된다.
2.  다른 문자열 s와 t가 있을 때, f(s)와 f(t)가 같은 문자열인 경우가 있다.  
    예를 들어서, s = "abc", t = "abcabc"인 경우에 f(s)와 f(t)는 같은 문자열을 만든다.
3.  s와 t가 주어졌을 때, f(s)와 f(t)가 같은 문자열을 만드는지 아닌지 구하는 문제.
4.  첫째 줄에 s, 둘째 줄에 t가 주어진다.  
    두 문자열 s와 t의 길이는 50보다 작거나 같은 자연수이고, 알파벳 소문자로만 이루어져 있다.
5.  첫째 줄에 f(s)와 f(t)가 같으면 1을, 다르면 0을 출력한다.
6.  **문자열, 구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
ab
abab
```

#### 실행결과 1

```py
1
```

#### 예제 2

```py
abc
bca
```

#### 실행결과 2

```py
0
```

<br>

### ⌨️ 문제 풀이

1.  각 문자의 길이를 구하고, 그 길이들의 최소 공배수를 구했다.
2.  최소공배수만큼 문자열의 길이를 늘리고 비교했다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from math import lcm

a = stdin.readline().rstrip()
b = stdin.readline().rstrip()
al, bl = len(a), len(b)
length = lcm(al, bl)
print(1 if a * (length // al) == b * (length // bl) else 0)
```