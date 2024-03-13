---
author: ["Jxun-h"]
title: "[BOJ] 11383 뚊 with Python"
date: "2023-04-13 15:08:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "문자열", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/11383" target="_blank">BOJ 11383 뚊</a>

<br>

### 💡 조건

1.  정우는 "뚊"과 "돌돔"을 의미하는 두 이미지를 받았다. 과연 두 그림이 같은지 검사해보자.
2.  즉 N× M 크기의 이미지와 N ×2 M 크기의 이미지가 주어질 때  
    첫 번째 이미지를 가로로 두 배로 늘이면 두 번째 이미지가 되는지 검사하는 프로그램을 작성하는 문제.
3.  입력의 첫 번째 줄에 N, M (1 ≤ N, M ≤ 10)이 주어진다.  
    다음 N개의 줄의 각 줄에는 M개의 문자가 주어진다.
4.  다음 N개의 줄의 각 줄에는 2M개의 문자가 주어진다. 모든 문자는 영문 알파벳 대문자 혹은 소문자이다.
5.  첫 번째로 주어진 이미지를 가로로 두 배로 늘렸을 때 두 번째 이미지가 된다면 "Eyfa"을 출력, 되지 않는다면 "Not Eyfa"을 출력
6.  **문자열, 구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
1 5
ABCDE
AABBCCDDEE
```

#### 실행결과 1

```py
Eyfa
```

#### 예제 2

```py
ABCDE
AABBCCDDEF
```

#### 실행결과 2

```py
Not Eyfa
```

#### 예제 3

```py
2 2
AB
CD
AABB
CCDD
```

#### 실행결과 3

```py
Eyfa
```

<br>

### ⌨️ 문제 풀이

1.  입력을 받은 문자열을 관리할 리스트를 생성해, n개 만큼 입력을 받는다.
2.  입력을 받은 문자열을 관리할 리스트에 넣기 전, 순회를 하면서 각 문자를 2개씩 이어붙인다.
3.  (1)~(2) 번에서 제작한 문자열과 이후에 입력 받은 비교할 문자열을 비교해, 하나라도 틀렸을 시, Not Eyfa 를 출력한다.
4.  함수를 하나 만들어 결과를 return 해주면 코드가 더 쉽다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

inp = stdin.readline
n, m = map(int, inp().split())
be, af = [], []

for i in range(n):
    res = ''
    s = stdin.readline().rstrip()
    for i in s:
        res += i * 2

    be.append(res)

for i in range(n):
    af.append(stdin.readline().rstrip())


def get_res():
    for i in range(n):
        if be[i] != af[i]:
            return 0

    return 1


print('Eyfa' if get_res() else 'Not Eyfa')
```