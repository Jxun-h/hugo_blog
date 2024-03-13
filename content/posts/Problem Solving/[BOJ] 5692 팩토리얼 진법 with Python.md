---
author: ["Jxun-h"]
title: "[BOJ] 5692 팩토리얼 진법 with Python"
date: "2023-04-03 16:04:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/5692" target="_blank">BOJ 5692 팩토리얼 진법</a>

<br>

### 💡 조건

1.  팩토리얼 진법에서는 i번 자리의 값을 ai×i!로 계산한다.
2.  즉, 팩토리얼 진법에서 719는 10진법에서 53과 같다. 그 이유는 7×3! + 1×2! + 9×1! = 53이기 때문이다.
3.  입력은 여러 개의 테스트 케이스로 이루어져 있다.  
    각 테스트 케이스는 한 줄로 이루어져 있고, 길이가 최대 5자리인 팩토리얼 진법 숫자가 주어진다.  
    입력의 마지막 줄에는 0이 하나 주어진다.
4.  각 테스트 케이스에 대해서, 입력으로 주어진 팩토리얼 진법 숫자를 10진법으로 읽은 값을 출력한다.
5.  **수학** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
719
1
15
110
102
0
```

#### 실행결과 1

```py
53
1
7
8
8
```

<br>

### ⌨️ 문제 풀이

1.  입력 받은 숫자를 문자열로 변경한 뒤, 길이(l)를 구한다.
2.  숫자를 한자리씩 순회하면서(i) i * l! 를 계산해 ans 에 더해준다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from math import factorial as fa

while 1:
    n = int(stdin.readline())
    if n == 0:
        break

    l = len(str(n))
    ans = 0

    for i in str(n):
        ans += fa(l) * int(i)
        l -= 1

    print(ans)
```