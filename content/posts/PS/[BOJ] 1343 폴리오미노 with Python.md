---
author: ["Jxun-h"]
title: "[BOJ] 1343 폴리오미노 with Python"
date: "2022-03-29"
description: ""
summary: ""
tags: ["자료구조", "PS", "문자열", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1343" target="_blank">BOJ 1343 폴리오미노</a>

<br>

### 💡 조건

1.  AAAA와 BB 폴리오미노 2개를 무한개만큼 가지고 있다.
2.  '.'와 'X'로 이루어진 보드판이 주어졌을 때, 민식이는 겹침없이 'X'를 모두 폴리오미노로 덮으려고 한다.  
    '.'는 폴리오미노로 덮으면 안 된다.
3.  폴리오미노로 모두 덮은 보드판을 출력하는 문제
4.  보드판의 크기는 최대 50이다.
5.  **문자열** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
XXXXXX
```

#### 실행결과

```py
AAAABB
```

<br>

### ⌨️ 문제 풀이

1.  AAAA 네개가 들어갈 수 있다면 먼저 XXXX를 AAAA로 변경해준다.
2.  그 후 XX를 BB로 변경해준다.
3.  변경 후에도 X가 남아있다면 -1 출력  
    없다면 변경된 문자를 출력

<br>

### 🖥 소스 코드

```py
from sys import stdin

p = stdin.readline().rstrip()
p = p.replace('XXXX', 'AAAA')
p = p.replace('XX', 'BB')

if 'X' in p:
    print(-1)
else:
    print(p)
```

<br>

### 💾 느낀점