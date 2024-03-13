---
author: ["Jxun-h"]
title: "[BOJ] 7600 문자가 몇갤까 with Python"
date: "2023-04-11 15:11:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "문자열", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/7600" target="_blank">BOJ 7600 문자가 몇갤까</a>

<br>

### 💡 조건

1.  각 케이스마다 문장에서 공백, 숫자, 특수 문자를 제외하고 얼마나 다양한 알파벳이 나왔는지를 구하는 문제.
2.  대소문자는 하나의 문자로 처리한다. ex) 'A' == 'a'
3.  입력은 250자를 넘지 않는 문장이 주어진다.
4.  각 문장은 적어도 하나의 공백이 아닌 문자를 포함한다. (알파벳이 아닐 수 있다)  
    마지막 줄에는 '#'이 주어진다.
5.  **문자열, 구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
The quick brown fox jumped over the lazy dogs.
2 + 2 = 4
New Zealand Programming Contest.
#
```

#### 실행결과 1

```py
26
0
16
```

<br>

### ⌨️ 문제 풀이

1.  입력받은 문장을 모두 소문자로 변환한 뒤 계산하면 편하다.
2.  알파벳이 나왔는지 체크할 방문처리 배열을 만들고, 문자열을 순회하면서 체크한다.
3.  체크를 1로 해두고 문자열 순회가 끝난 뒤 방문처리 배열을 sum() 한 결과값을 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

while 1:
    s = stdin.readline().rstrip().lower()
    a = [0 for _ in range(26)]
    if s == '#':
        break
    for i in s:
        n = ord(i)
        if 97 <= n <= 122:
            if a[n - 97] == 0:
                a[n - 97] = 1

    print(sum(a))
```