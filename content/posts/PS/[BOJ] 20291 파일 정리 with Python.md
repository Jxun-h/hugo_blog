---
author: ["Jxun-h"]
title: "[BOJ] 20291 파일 정리 with Python"
date: "2022-01-26"
description: ""
summary: ""
tags: ["자료구조", "PS", "해시맵", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/20291" target="_blank">BOJ 20291 파일 정리</a>

<br>

### 💡 조건

1.  바탕화면에 있는 파일의 개수 N (1 <= N <= 50000)
2.  파일의 이름은 알파벳 소문자와 점(.)으로만 구성되어 있다.  
    점은 정확히 한 번 등장하며, 파일 이름의 첫 글자 또는 마지막 글자로 오지 않는다.  
    각 파일의 이름의 길이는 최소 3, 최대 100이다.
3.  확장자의 이름과 그 확장자 파일의 개수를 한 줄에 하나씩 출력한다.  
    확장자가 여러 개 있는 경우 확장자 이름의 사전순으로 출력한다.
4.  **해시맵 자료구조 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
8
sbrus.txt
spc.spc
acm.icpc
korea.icpc
sample.txt
hello.world
sogang.spc
example.txt
```

#### 실행결과

```py
icpc 2
spc 2
txt 3
world 1
```

<br>

### ⌨️ 문제 풀이

1.  확장자의 이름과 개수를 저장할 dict 자료형 변수 하나를 만든다.
2.  split() 함수를 사용해 '.'을 기준으로 분리한 후 확장자 명이 dict에 있을 경우 + 1, 없으면 새로 추가한 후 1값을 넣는다.
3.  dict\_name.items() 함수를 사용하여, key, value 쌍을 res 리스트에 넣고 정렬한 뒤 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
file_name = {}
for i in range(n):
    data = stdin.readline().rstrip().split('.')
    if data[1] in file_name:
        file_name[data[1]] += 1
    else:
        file_name[data[1]] = 1

res = []
for key, item in file_name.items():
    res.append((key, item))

res.sort()
for i in res:
    print(*i)
```

<br>

### 💾 느낀점

1.  해시맵을 사용해 간단하게 풀었던 문제였습니다.