---
author: ["Jxun-h"]
title: "[BOJ] 1759 암호 만들기 with Python"
date: "2022-02-13"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "백트래킹", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1759" target="_blank">BOJ 1759 암호 만들기</a>

<br>

### 💡 조건

1.  암호는 서로 다른 L개의 알파벳 소문자들로 구성되며 최소 한 개의 모음(a, e, i, o, u)과  
    최소 두 개의 자음으로 구성되어 있다고 알려져 있다.
2.  암호를 이루는 알파벳이 암호에서 증가하는 순서로 배열되었을 것.  
    즉, abc는 가능성이 있는 암호이지만 bac는 그렇지 않다.
3.  C개의 문자들이 모두 주어졌을 때, 가능성 있는 암호들을 모두 구하는 프로그램을 작성.  
    각 줄에 하나씩, 사전식으로 가능성 있는 암호를 모두 출력
4.  두 정수 L, C가 주어진다. (3 ≤ L ≤ C ≤ 15)
5.  문자들은 알파벳 소문자이며, 중복되는 것은 없다.
6.  **브루트포스, 백트래킹** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4 6
a t c i s w
```

#### 실행결과

```py
acis
acit
aciw
acst
acsw
actw
aist
aisw
aitw
astw
cist
cisw
citw
istw
```

<br>

### ⌨️ 문제 풀이

1.  L, C 를 입력받고, C 개의 암호로 사용되었을 법한 문자를 리스트로 입력받는다.
2.  C 개의 암호로 사용되었을 법한 문자를 순회하면서, 모음 (a, e, i, o, u) 가 있는지 확인하여  
    mo_um 리스트에 저장한다.
3.  결과를 저장할 res 변수를 중복을 방지하기 위해 set() 자료형으로 생성한다.
4.  combinations 함수를 사용해 l의 길이로 된 조합을 만든다. set() 으로 감싸서 중복을 제거해준다.
5.  length 변수에 l을 저장해주고, 만들어진 조합을 순회한다.(i)  
    mo_um을 순회하면서 i에 해당 모음이 있는지 확인하고, 있다면 length - 1 해준다.
6.  암호는 최소 한 개의 모음을 가지고 있고, 두 개 이상의 자음을 가지고 있어야 한다.  
    length 가 2보다 작거나 l과 같을 경우 continue 해주고, 아니라면 res에 저장한다.
7.  res 를 한줄씩 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from itertools import combinations

mo_um = []

l, c = map(int, stdin.readline().split())
alpha = list(stdin.readline().rstrip().split())

for i in alpha:
    if i in ("a", "e", "i", "o", "u"):
        mo_um.append(i)

res = set()
for i in list(set(combinations(alpha, l))):
    length = l
    for k in mo_um:
        if k in i:
            length -= 1
    if length < 2 or length == l:
        continue
    else:
        res.add(tuple(sorted(list(i))))

for i in list(sorted(res)):
    print(''.join(i))
```

<br>

### 💾 느낀점

1.  약 7회 시도 끝에 정답을 맞췄습니다.  
    조건문이 잘못되어 틀렸습니다.
2.  length 변수를 만들어 조건을 사용할 생각을 하지 못해서 틀린 경우가 많았습니다.
3.  다른 골드 난이도보다는 조금 쉬운 난이도의 문제였던 것 같습니다.
4.  브루트포스, 백트래킹 문제를 더 많이 풀어보고 경험해봐야할 것 같습니다.