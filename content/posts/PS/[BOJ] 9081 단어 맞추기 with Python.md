---
author: ["Jxun-h"]
title: "[BOJ] 9081 단어 맞추기 with Python"
date: "2022-03-09"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/9081" target="_blank">BOJ 9081 단어 맞추기</a>

<br>

### 💡 조건

1.  단어를 주면 그 단어를 이루는 알파벳들로 만들 수 있는 단어들을 사전 순으로 정렬할 때에  
    주어진 단어 다음에 나오는 단어를 찾는 프로그램을 작성하는 문제
2.  케이스의 개수 T (1 ≤ T ≤ 10)
3.  단어는 알파벳 A~Z 대문자로만 이루어지며 항상 공백이 없는 연속된 알파벳으로 이루어진다.  
    단어의 길이는 100을 넘지 않는다.
4.  **구현** 유형의 문제

<br>

### 🖥 소스 코드

```py
from sys import stdin

for t in range(int(stdin.readline())):
    string = list(stdin.readline().rstrip())
    length = len(string)
    i, j = 0, 1
    for idx in range(1, length):
        if string[idx] > string[idx - 1]:
            if i < idx:
                i = idx

    for idx in range(1, length):
        if string[idx] > string[i - 1]:
            if j < idx:
                j = idx

    if i != 0 and j != 0:
        string[i-1], string[j] = string[j], string[i-1]

        string[i:] = list(reversed(string[i:]))
    print(''.join(string))
```

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4
HELLO
DRINK
SHUTTLE
ZOO
```

#### 실행결과

```py
HELOL
DRKIN
SLEHTTU
ZOO
```

<br>

### ⌨️ 문제 풀이

1.  s[i-1] < s[i] 를 만족하는 최대 i(s의 value) 찾는다.
2.  j >= 1, s[i-1] < s[j] 를 만족하는 최대 j(index) 찾는다.
3.  s[i-1] 과 s[j] 를 바꿔준 뒤, s[i:]의 데이터를 뒤집어 준다.

<br>

### 💾 느낀점

1.  문제를 풀기 위해서 다음에 오는 문자를 구하기 위한 공식이 따로 있었습니다.
2.  cpp 에서는 next_permutation 을 사용해서 풀면 된다고 했던 것 같은데, 파이썬은 그게 없다.