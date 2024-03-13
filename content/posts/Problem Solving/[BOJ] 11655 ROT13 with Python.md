---
author: ["Jxun-h"]
title: "[BOJ] 11655 ROT13 with Python"
date: "2022-02-10"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "문자열", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/11655" target="_blank">BOJ 11655 ROT13</a>

<br>

### 💡 조건

1.  ROT13은 카이사르 암호의 일종으로 영어 알파벳을 13글자씩 밀어서 만든다.  
    "Baekjoon Online Judge"를 ROT13으로 암호화하면 "Onrxwbba Bayvar Whqtr"가 된다.  
    ROT13으로 암호화한 내용을 원래 내용으로 바꾸려면 암호화한 문자열을 다시 ROT13하면 된다.
2.  S를 ROT13으로 암호화한 내용을 출력하는 문제
3.  **구현, 문자열**유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
Baekjoon Online Judge
```

#### 실행결과

```py
Onrxwbba Bayvar Whqtr
```

<br>

### ⌨️ 문제 풀이

1.  각 문자열을 순회하면서 아스키코드에 해당하는 숫자를 대문자일 경우와 소문자일 경우를 나눠 처리를 하고  
    각 아스키코드 숫자에 +13을 해주어 바꾸어주고 출력하면 된다.
2.  만약 아스키코드 숫자가 알파벳 문자 범위를 넘어간다면, -26을 해주어 다시 그 범위안으로 들어가주게 한 뒤 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

for i in list(stdin.readline().rstrip()):
    if i == ' ':
        print(' ', end='')
    elif i.isnumeric():
        print(i, end='')
    else:
        if i.isupper():
            temp = ord(i) + 13
            if temp > 90:
                print(chr(temp - 26), end='')
            else:
                print(chr(temp), end='')
        else:
            temp = ord(i) + 13
            if temp > 122:
                print(chr(temp - 26), end='')
            else:
                print(chr(temp), end='')
```

<br>

### 💾 느낀점

1.  재미있는 문자열, 구현 문제였습니다.