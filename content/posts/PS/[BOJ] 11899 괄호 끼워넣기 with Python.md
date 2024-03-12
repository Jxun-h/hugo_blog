---
author: ["Jxun-h"]
title: "[BOJ] 11899 괄호 끼워넣기 with Python"
date: "2022-03-16"
description: ""
summary: ""
tags: ["자료구조", "PS", "문자열", "스택", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/11899" target="_blank">BOJ 11899 괄호 끼워넣기</a>

<br>

### 💡 조건

1.  올바르지 않은 괄호열이 주어질 때, 올바른 괄호열으로 만들기 위해 앞과 뒤에 붙여야 할 괄호의 최소 개수를 구하는 문제.
2.  S의 길이는 1 이상 50 이하이며 불가능한 경우는 주어지지 않는다.
3.  괄호열이란 여는 괄호 ‘(’와 닫는 괄호 ‘)’로만 구성된 문자열을 말합니다.
4.  올바른 괄호열은 아래와 같이 정의할 수 있다.
    -   "()"는 올바른 괄호열입니다.
    -   A가 올바른 괄호열이라면 "(A)" 역시 올바른 괄호열입니다.
    -   A와 B가 모두 올바른 괄호열이라면 "AB" 역시 올바른 괄호열입니다.
5.  **문자열, 스택, 자료구조** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
))()((
```

#### 실행결과

```py
4
```

<br>

### ⌨️ 문제 풀이

1.  문자열을 입력받아 solve() 함수를 거쳐 cnt에 저장된 값을 출력한다.
2.  solve() 는 문자열을 역순회하며 닫는 괄호의 수를 세며 temp 에 저장한다.
3.  만약 순회하는 중, 닫는 괄호가 아닐 경우 또한 temp가 0일 경우, cnt + 1
4.  만약 순회하는 중, 닫는 괄호가 아닐 경우 또한 temp가 0이 아닐 경우, temp - 1
5.  순회가 끝난 후에 temp 가 0이 아니라면 cnt 에 temp를 더해준다.
6.  cnt 출력

<br>

### 🖥 소스 코드

```py
from sys import stdin

g = stdin.readline().rstrip()
cnt = 0


def solve(s):
    global cnt
    temp = 0
    for i in range(len(s) - 1, -1, -1):
        if s[i] == ')':
            temp += 1
        else:
            if temp - 1 < 0:
                cnt += 1
            else:
                temp -= 1

    if temp != 0:
        cnt += temp


solve(g)
print(cnt)
```

<br>

### 💾 느낀점

1.  프로그래머스에서 괄호 변환 등의 문제를 풀면서 고생을 해서 그런지, 감각은 확실이 깨어 있는 듯하다.