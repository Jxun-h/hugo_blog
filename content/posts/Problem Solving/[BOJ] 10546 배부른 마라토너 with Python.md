---
author: ["Jxun-h"]
title: "[BOJ] 10546 배부른 마라토너 with Python"
date: "2022-02-24"
description: ""
summary: ""
tags: ["자료구조", "PS", "해시맵", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/10546" target="_blank">BOJ 10546 배부른 마라토너</a>

<br>

### 💡 조건

1.  참가자 수 N이 주어진다. (1 ≤ N ≤ 105)
2.  N개의 줄에는 참가자의 이름이 주어진다.
3.  N-1개의 줄에는 완주한 참가자의 이름이 쓰여져 있다.
4.  참가자들의 이름은 길이가 1보다 크거나 같고, 20보다 작거나 같은 문자열이고, 알파벳 소문자로만 이루어져 있다.  
    **참가자들 중엔 동명이인이 있을 수도 있다.**
5.  백준 마라톤 대회에 참가해 놓고 완주하지 못한 배부른 참가자 한 명은 누굴까?
6.  **해시맵 자료구조 응용** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4
mislav
stanko
mislav
ana
stanko
ana
mislav
```

#### 실행결과

```py
mislav
```

<br>

### ⌨️ 문제 풀이

1.  동명이인이 있다는 것이 중요합니다. {key: value} 형식으로 저장되는 데이터를 사용하는 Dictionary 자료구조를 사용합니다.
2.  n 을 입력받고, n만큼 반복문을 진행하면서 대회에 참가한 인원들을 dictionary 자료구조에 넣습니다.  
    {참가자 이름 : 인원 수}, 인원 수는 dictionary 에 이름이 없을 땐 1로 초기화해서 넣습니다.
3.  n-1 만큼 반복문을 진행하면서 완주한 사람들의 이름에 해당하는 값을 dictionary에서 -1 해줍니다.
4.  dictionary.item() 을 통해서 key, value 값을 순회하면서 value 가 0보다 큰 키 값을 찾습니다.
5.  참가자 한명을 찾는 것이기 때문에 출력한 뒤 바로 break 를 걸어 멈춰줍니다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
mara_tang = {}

for _ in range(n):
    name = stdin.readline().rstrip()
    if name not in mara_tang:
        mara_tang[name] = 1
    else:
        mara_tang[name] += 1

for _ in range(n - 1):
    mara_tang[stdin.readline().rstrip()] -= 1

for key, item in mara_tang.items():
    if item != 0:
        print(key)
        break
```

<br>

### 💾 느낀점

1.  파이썬 딕셔너리 만세