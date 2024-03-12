---
author: ["Jxun-h"]
title: "[BOJ] 6603 로또 with Python"
date: "2022-02-10"
description: ""
summary: ""
tags: ["자료구조", "PS", "백트래킹", "재귀", "조합", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/6603" target="_blank">BOJ 6603 로또</a>

<br>

### 💡 조건

1.  집합 S에서 K개의 숫자를 골라 뽑아 낼 수 있는 경우의 수를 모두 출력하는 문제
2.  입력이 여러개 들어오며, 0이 들어왔을 때 종료
3.  **백트래킹, 재귀, 조합**유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
7 1 2 3 4 5 6 7
8 1 2 3 5 8 13 21 34
0
```

#### 실행결과

```py
1 2 3 4 5 6
1 2 3 4 5 7
1 2 3 4 6 7
1 2 3 5 6 7
1 2 4 5 6 7
1 3 4 5 6 7
2 3 4 5 6 7

1 2 3 5 8 13
1 2 3 5 8 21
1 2 3 5 8 34
1 2 3 5 13 21
1 2 3 5 13 34
1 2 3 5 21 34
1 2 3 8 13 21
1 2 3 8 13 34
1 2 3 8 21 34
1 2 3 13 21 34
1 2 5 8 13 21
1 2 5 8 13 34
1 2 5 8 21 34
1 2 5 13 21 34
1 2 8 13 21 34
1 3 5 8 13 21
1 3 5 8 13 34
1 3 5 8 21 34
1 3 5 13 21 34
1 3 8 13 21 34
1 5 8 13 21 34
2 3 5 8 13 21
2 3 5 8 13 34
2 3 5 8 21 34
2 3 5 13 21 34
2 3 8 13 21 34
2 5 8 13 21 34
3 5 8 13 21 34
```

<br>

### ⌨️ 문제 풀이

1.  조합을 이용하여 S 수열에 있는 K개의 숫자를 뽑아낸 조합의 경우의 수를 구하되, 가능한 조합을 모두 출력하는 문제.
2.  combinations 를 사용하여 조합을 모두 뽑아내고, res 라는 리스트에 넣어 출력했다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from itertools import combinations

while 1:
    data = list(map(int, stdin.readline().split()))
    if len(data) == 1 and data[0] == 0:
        break
    else:
        a, arr = data[0], data[1:]
        res = []
        for x in list(set(combinations(arr, 6))):
            if len(set(x)) == 6:
                temp = sorted(list(x))
                if temp not in res:
                    res.append(temp)

    for x in sorted(list(res)):
        print(*x)
    print()
```

<br>

### 💾 느낀점

1.  백트래킹 문제는 재귀로 풀어보는 것이 도움이 된다.
2.  N과 M 시리즈를 풀면서 재귀로 백트래킹을 연습하는 것도 좋을 것 같다.