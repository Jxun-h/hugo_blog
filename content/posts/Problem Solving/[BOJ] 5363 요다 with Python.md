---
author: ["Jxun-h"]
title: "[BOJ] 5363 요다 with Python"
date: "2023-04-13 11:30:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "문자열", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/5363" target="_blank">BOJ 5363 요다</a>

<br>

### 💡 조건

1.  어린 제다이들은 요다와 대화하는 법을 배워야 한다. 요다는 모든 문장에서 가장 앞 단어 두 개를 제일 마지막에 말한다.
2.  어떤 문장이 주어졌을 때, 요다의 말로 바꿔 출력하는 문제.
3.  첫째 줄에 문장의 수 N이 주어진다. 둘째 줄부터 N개의 줄에는 각 문장이 주어진다.
4.  문장의 길이는 100글자 이내이다. 단어의 개수는 3개 이상이다.
5.  **문자열, 구현** 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```text
4
I will go now to find the Wookiee
Solo found the death star near planet Kessel
I'll fight Darth Maul here and now
Vader will find Luke before he can escape
```

#### 실행결과 1

```text
go now to find the Wookiee I will
the death star near planet Kessel Solo found
Darth Maul here and now I'll fight
find Luke before he can escape Vader will
```

<br>

### ⌨️ 문제 풀이

1.  [:2]에 해당하는 문자를 [2:] 에 해당하는 문자열 뒤에 붙여주면 된다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

for _ in range(int(stdin.readline())):
    a = list(stdin.readline().rstrip().split())
    print(*(a[2:] + a[:2]))
```