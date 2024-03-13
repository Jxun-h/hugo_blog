---
author: ["Jxun-h"]
title: "[BOJ] 4740 거울, 오! 거울 with Python"
date: "2023-04-03 13:25:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "문자열", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/4740" target="_blank">BOJ 4740 거울, 오! 거울</a>

<br>

### 💡 조건

1.  문장을 입력하면 입력한 문장의 개별 단어들을 역순으로 배치하여  
    거꾸로 바뀐 문장을 출력하는 프로그램을 만들어 '거울 읽기' 연습을 하려고 마음먹었다.
2.  하나 또는 그 이상의 줄에 각각 ASCII 글자로 나타낼 수 있는 단어들(알파벳, 숫자, 공백, 구두점 등)로 구성된 문장을 입력한다.
3.  각 문장은 최소 1글자에서 최대 80글자로 이루어져 있으며, ***을 입력하면 프로그램이 종료된다.
4.  한 문장의 입력이 끝난 뒤 바로 입력한 문장의 글자들이 역순으로 바뀌어 배치된 문장을 출력한다.
5.  **문자열, 구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```text
AMBULANCE
Evian
madam, i'm adam
***
```

#### 실행결과 1

```text
ECNALUBMA
naivE
mada m'i ,madam
```

<br>

### ⌨️ 문제 풀이

1.  rstrip() 으로 문자열을 받으면 공백까지 지워지는 현상이 있다. 그러니, rstrip('n')으로 받자.
2.  reverse() 함수를 쓸 필요가 없다.  
    [::-1] 로 역순 출력이 가능하다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

while 1:
    s = stdin.readline().rstrip('n')
    if s == '***':
        break
    print(s[::-1])
```