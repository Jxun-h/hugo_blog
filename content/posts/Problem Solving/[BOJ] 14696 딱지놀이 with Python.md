---
author: ["Jxun-h"]
title: "[BOJ] 14696 딱지놀이 with Python"
date: "2022-05-11"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/14696" target="_blank">BOJ 14696 딱지놀이</a>

<br>

### 💡 조건

1.  4, 3, 2, 1 에 해당하는 숫자가 각 몇 개인지 파악하여 승자가 누구인지 출력하는 문제
2.  서브태크스가 존재한다.
3.  출력의 i번째 (1 ≤ i ≤ N) 줄에 정확히 한 글자를 출력하는데, 출력하는 글자는 A, B, D 중 하나로 라운드 i의 결과를 나타낸다.
4.  각 라운드의 결과는 A가 승자라면 A, B가 승자라면 B, 무승부라면 D이다.
5.  **구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5
1 4
4 3 3 2 1
5 2 4 3 2 1
4 4 3 3 1
4 3 2 1 1
4 2 3 2 1
4 4 3 2 1
3 4 3 2
5 4 4 2 3 1
5 4 2 4 1 3
```

#### 실행결과

```py
A
B
B
A
D
```

<br>

### 🖥 소스 코드

```py
from sys import stdin

for _ in range(int(stdin.readline())):

    a = list(map(int, stdin.readline().split()))[1:]
    b = list(map(int, stdin.readline().split()))[1:]

    _4a, _4b = a.count(4), b.count(4)
    if _4a == _4b:
        _3a, _3b = a.count(3), b.count(3)
        if _3a == _3b:
            _2a, _2b = a.count(2), b.count(2)
            if _2a == _2b:
                _1a, _1b = a.count(1), b.count(1)
                if _1a == _1b:
                    print('D')
                else:
                    print('A') if _1a > _1b else print('B')
            else:
                print('A') if _2a > _2b else print('B')
        else:
            print('A') if _3a > _3b else print('B')
    else:
        print('A') if _4a > _4b else print('B')
```
