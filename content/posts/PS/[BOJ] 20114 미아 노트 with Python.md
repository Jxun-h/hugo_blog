---
author: ["Jxun-h"]
title: "[BOJ] 20114 미아 노트 with Python"
date: "2022-05-15"
description: ""
summary: ""
tags: ["자료구조", "PS", "문자열", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/20114" target="_blank">BOJ 20114 미아 노트</a>

<br>

### 💡 조건

1.  노트에 적힌 문자열이 번진 패턴은 일정했는데, 가령 "abc" 문자가 세로로 3글자씩, 가로로 2글자씩 번진 경우는 다음과 같았다.
2.  아쉽게도 번진 문자열의 일부는 지워진 상태였다.  
    너무 많이 지워져버려서 해당 자리의 문자를 유추할 수 없는 경우, 완전히 문자열을 복원하지 못할 수도 있다.
3.  첫째 줄에 원래 문자열의 길이 N, 세로로 번진 글자의 개수 H, 가로로 번진 글자의 개수 W가 주어진다.  
    (1 ≤ N ≤ 100, 1 ≤ H ≤ 10, 1 ≤ W ≤ 10)
4.  H개의 줄에 걸쳐 N × W 길이의 문자열이 주어진다.  
    문자열은 알파벳 소문자 또는 '?'로만 이루어져 있다.  
    '?'는 해당 자리의 문자가 지워진 경우를 뜻한다.
5.  문자가 번진 자리에 두 개 이상의 문자가 있는 등 모순되는 경우는 입력으로 주어지지 않는다.
6.  **문자열, 구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
6 2 3
???rrruuu???ttt???
f?f?rruuu?????t???
```

#### 실행결과

```py
fru?t?
```

<br>

### ⌨️ 문제 풀이

1.  원래의 문자열의 길이를 복원하는 문제이다.
2.  원래의 문자열의 길이만큼 반복하면서 해당 문자열의 위치(변수 x) 부터 번진만큼 반복문을 통해 원래 문자를 찾는다.
3.  원래 문자열의 위치 x부터 가로로 번진만큼 반복하고, 세로로 번진만큼 또 반복을 하면서 원래 문자열을 지금 찾을 수 있는지 알아본다.
4.  ans에 문자열을 찾을 수 있다면 찾은 해당 문자열을 넣고, 아니라면 ? 를 넣는다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, h, w = map(int, stdin.readline().split())
arr = [list(stdin.readline().rstrip()) for _ in range(h)]


def solve(x):
    global ans
    for i in range(x * w, (x + 1) * w):
        for j in range(h):
            if arr[j][i] != '?':
                ans += arr[j][i]
                return
    ans += '?'
    return


ans = ''
for i in range(n):
    solve(i)
print(ans)
```
