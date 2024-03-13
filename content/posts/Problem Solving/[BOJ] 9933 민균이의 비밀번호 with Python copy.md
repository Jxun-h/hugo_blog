---
author: ["Jxun-h"]
title: "[BOJ] 9933 민균이의 비밀번호 with Python"
date: "2022-02-02"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "문자열", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/9933" target="_blank">BOJ 9933 민균이의 비밀번호</a>

<br>

### 💡 조건

1.  민균이의 비밀번호가 "tulipan"인 경우에 목록에는 "napilut"도 존재해야 한다.
2.  민균이의 파일에 적혀있는 단어가 모두 주어졌을 때, 비밀번호의 길이와 가운데 글자를 출력하는 프로그램을 작성하라.
3.  단어의 수 N (2 ≤ N ≤ 100)이 주어진다.
4.  단어는 알파벳 소문자로만 이루어져 있으며, 길이는 2보다 크고 14보다 작은 홀수이다.
5.  **구현, 문자열 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4
las
god
psala
sal
```

#### 실행결과

```py
3 a
```

<br>

### ⌨️ 문제 풀이

1.  data 리스트에 입력되는 n개의 비밀번호를 저장한다.
2.  temp 변수에 data 리스트의 i번째 비밀번호를 복사한다.  
    temp에 있는 리스트를 뒤집어준다.
3.  temp가 만약 data 안에 있다면, data 의 가운데 글자와 비밀번호의 길이를 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
data = []
for _ in range(n):
    data.append(list(stdin.readline().rstrip()))


def solve():
    for i in range(n):
        temp = data[i][:]
        temp.reverse()
        if temp in data:
            length = len(temp)
            mid = data[i][length // 2]
            return length, mid


print(*solve())
```

<br>

### 💾 느낀점

1.  간단한 구현 및 문자열 문제였습니다.