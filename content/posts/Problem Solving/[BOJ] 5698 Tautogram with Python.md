---
author: ["Jxun-h"]
title: "[BOJ] 5698 Tautogram with Python"
date: "2022-03-16"
description: ""
summary: ""
tags: ["자료구조", "PS", "문자열", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/5698" target="_blank">BOJ 5698 Tautogram</a>

<br>

### 💡 조건

1.  Tautogram은 매우 특별한 형태의 두운법으로, 인접한 단어가 같은 글자로 시작하는 것을 말한다.
2.  문장이 Tautogram이 되려면, 모든 단어가 같은 글자로 시작해야 한다.
3.  선영이의 편지에 있는 문장이 주어졌을 때, Tautogram인지 아닌지 알아내는 프로그램을 작성하시오.
4.  문장은 최대 50개의 단어로 이루어져 있으며, 공백으로 구분되어져 있다.
5.  단어는 알파벳 대문자와 소문자로 이루어져 있고, 길이는 최대 20이다.
6.  마지막 테스트 케이스의 다음 줄에는 '*'이 하나 주어진다.  
    입력으로 주어진 문장이 Tautogram이라면 'Y'를, 아니라면 'N'을 출력한다.
7.  **문자열** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
Flowers Flourish from France
Sam Simmonds speaks softly
Peter pIckEd pePPers
truly tautograms triumph
this is NOT a tautogram
*
```

#### 실행결과

```py
Y
Y
Y
Y
N
```

<br>

### ⌨️ 문제 풀이

1.  검사할 문자열을 검사한다. 검사한 문자열이 * 이라면 반복문을 멈춘다.
2.  문자열을 공백으로 나누어서 체크할 문자열을 뽑는다.  
    모든 단어가 같은 문자열로 시작해야하기 때문에 맨 첫번째 단어의 첫번째 글자를 뽑아 소문자로 변경하여 chk에 저장한다.
3.  각 단어를 순회하면서 단어의 첫글자를 chk 와 비교하여 다르면 단어 순회를 중단하고 tf를 False 로 갱신.
4.  tf 가 True 라면 'Y'
5.  tf 가 False 라면 'Y'

<br>

### 🖥 소스 코드

```py
from sys import stdin

while 1:
    data = stdin.readline().rstrip()
    if data == '*':
        break
    words = data.split()
    chk = words[0][0].lower()
    tf = True
    for i in range(1, len(words)):
        if words[i][0].lower() != chk:
            tf = False
            break

    print('Y') if tf else print('N')
```

<br>

### 💾 느낀점