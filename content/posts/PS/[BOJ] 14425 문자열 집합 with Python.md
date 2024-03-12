---
author: ["Jxun-h"]
title: "[BOJ] 14425 문자열 집합 with Python"
date: "2022-02-27"
description: ""
summary: ""
tags: ["자료구조", "PS", "문자열", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/14425" target="_blank">BOJ 14425 문자열 집합</a>

<br>

### 💡 조건

1.  N개의 문자열로 이루어진 집합 S
2.  입력으로 주어지는 M개의 문자열 중에서 집합 S에 포함되어 있는 것이 총 몇 개인지 구하는 문제
3.  N과 M (1 ≤ N ≤ 10,000, 1 ≤ M ≤ 10,000)
4.  어지는 문자열은 알파벳 소문자로만 이루어져 있으며, 길이는 500을 넘지 않는다.
5.  집합 S에 같은 문자열이 여러 번 주어지는 경우는 없다.
6.  **문자열, 자료구조** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5 11
baekjoononlinejudge
startlink
codeplus
sundaycoding
codingsh
baekjoon
codeplus
codeminus
startlink
starlink
sundaycoding
codingsh
codinghs
sondaycoding
startrink
icerink
```

#### 실행결과

```py
4
```

<br>

### ⌨️ 문제 풀이

1.  n개의 문자열을 dictionary 자료형 변수에 넣는다
2.  m 개의 문자열을 입력 받으면서 만약 입력 받은 문자열이 만들어둔 dictionary 변수에 있다면  
    그 키에 해당하는 value 값을 + 1 해준다.
3.  dictionary 의 values 값을 모두 더해준다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = map(int, stdin.readline().split())
strings = {}

for _ in range(n):
    strings[stdin.readline().rstrip()] = 0

for i in range(m):
    s = stdin.readline().rstrip()
    if s in strings:
        strings[s] += 1

print(sum(strings.values()))
```

<br>

### 💾 느낀점

1.  해시맵, dict 자료구조를 이용하는 문제인데, 문제 태그에 트라이라고 되어 있었습니다.
2.  트라이까지 필요한지는 모르겠으나, N 과 M 의 최대 크기가 10000 이라서  
    dict 안에 입력 받은 m개의 문자열이 있는지 검사시켰습니다.