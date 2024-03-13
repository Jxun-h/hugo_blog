---
author: ["Jxun-h"]
title: "[BOJ] 1992 쿼드트리 with Python"
date: "2023-03-31 17:57:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "분할정복", "재귀", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1992" target="_blank">BOJ 1992 쿼드트리</a>

<br>

### 💡 조건

1.  주어진 영상이 모두 0으로만 되어 있으면 압축 결과는 "0"이 되고, 모두 1로만 되어 있으면 압축 결과는 "1"이 된다.
2.  만약 0과 1이 섞여 있으면 전체를 한 번에 나타내지를 못한다.  
    왼쪽 위, 오른쪽 위, 왼쪽 아래, 오른쪽 아래, 이렇게 4개의 영상으로 나누어 압축하게 된다.  
    이 4개의 영역을 압축한 결과를 차례대로 괄호 안에 묶어서 표현.
3.  N 은 언제나 2의 제곱수로 주어지며, 1 ≤ N ≤ 64의 범위를 가진다.
4.  N ×N 크기의 영상이 주어질 때, 이 영상을 압축한 결과를 출력하는 프로그램을 작성하는 문제.
5.  **분할정복, 재귀** 유형의 문제.

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
8
11110000
11110000
00011100
00011100
11110000
11110000
11110011
11110011
```

#### 실행결과 1

```py
((110(0101))(0010)1(0001))
```

<br>

### ⌨️ 문제 풀이

1.  분할정복의 개념으로 해결을 할 수 있는 문제이다.
2.  n 을 2씩 나누어 재귀를 통해 큰 단위에서 작은 단위로 가는 방식으로 해결했다.
3.  check() 함수로 각 좌표를 기준으로 mode 만큼 떨어진 좌표까지 숫자가 같은지 탐색한다.  
    만약 같지 않다면, 괄호를 넣고 재귀한다.
4.  같다면 1혹은 0을 넣어준다.
5.  좌표는 네 방향이다. 재귀를 할 때마다 mode는 두 배씩 줄어든다.

<br>

### 🖥 소스 코드

```py
from sys import stdin, setrecursionlimit

setrecursionlimit(10 ** 6)

n = int(stdin.readline())
arr, ans = [], ''
for i in range(n):
    arr.append(list(map(int, list(stdin.readline().rstrip()))))


def check(x, y, mode):
    for i in range(x, x + mode):
        for j in range(y, y + mode):
            if arr[x][y] != arr[i][j]:
                return False
    return True


def solve(x, y, mode):
    global ans

    if check(x, y, mode):
        if arr[x][y] == 1:
            ans += '1'
        else:
            ans += '0'

    else:
        ans += '('
        solve(x, y, mode // 2)
        solve(x, y + mode // 2, mode // 2)
        solve(x + mode // 2, y, mode // 2)
        solve(x + mode // 2, y + mode // 2, mode // 2)
        ans += ')'


solve(0, 0, n)
print(ans)
```