---
author: ["Jxun-h"]
title: "[BOJ] 6443 애너그램 with Python"
date: "2022-03-02"
description: ""
summary: ""
tags: ["자료구조", "PS", "백트래킹", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/6443" target="_blank">BOJ 6443 애너그램</a>

<br>

### 💡 조건

1.  첫째 줄에 단어의 개수 N 이, 둘째 줄부터 N개의 영단어가 들어온다.
2.  영단어는 소문자로 이루어져 있다. 단어의 길이는 20보다 작거나 같고, 애너그램의 수가 100,000개 이하인 단어만 입력으로 주어진다.
3.  애너그램 프로그램이란, 입력받은 영단어의 철자들로 만들 수 있는 모든 단어를 출력하는 것이다.
4.  입력받은 단어내에 몇몇 철자가 중복될 수 있다. 이 경우 같은 단어가 여러 번 만들어 질 수 있는데,
5.  한 번만 출력해야 한다. 또한 출력할 때에 알파벳 순서로 출력해야 한다.
6.  **백트래킹** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
2
abc
acba
```

#### 실행결과

```py
abc
acb
bac
bca
cab
cba
aabc
aacb
abac
abca
acab
acba
baac
baca
bcaa
caab
caba
cbaa
```

<br>

## ⌨️# 문제 풀이

1.  string 이라는 변수에 문자열을, 각 알파벳이 몇 개 나왔는지 개수를 저장할 alpha 라는 변수를 만든다
2.  입력받은 문자열을 순회하면서 arr에 각 알파벳의 개수를 기록해준다.
3.  solve() 함수에 string의 길이와 빈 문자열을 매개변수로 주고 실행합니다.
4.  solve() 함수에서 alpha 배열의 값이 0보다 클 때 매개변수로 문자열에 알파벳을 붙이고 매개변수로 넣는다.  
    그리고 문자열의 길이를 -1 해준다.
5.  매개변수로 받는 문자열의 길이가 0이 되었을 때, visited 에 넣어줍니다.
6.  visited 를 리스트로 변환하고, 정렬한 뒤, 순서대로 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin


def solve(l, s):
    if l == 0:
        visited.add(s)
        return

    for i in range(26):
        if alpha[i] >= 1:
            alpha[i] -= 1
            solve(l - 1, s + chr(i + 97))
            alpha[i] += 1


for _ in range(int(stdin.readline())):
    visited = set()
    alpha = [0 for _ in range(26)]
    string = stdin.readline().rstrip()

    for i in string:
        alpha[ord(i)-97] += 1

    solve(len(string), '')
    for s in sorted(list(visited)):
        print(s)
```

<br>

### 💾 느낀점

1.  골드문제치고 시간초과가 나지 않는 쉬운 문제였습니다.
2.  재귀함수를 통해서 백트래킹으로 간단히 풀 수 있는 문제였습니다.