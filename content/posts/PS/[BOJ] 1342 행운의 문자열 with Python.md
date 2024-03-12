---
author: ["Jxun-h"]
title: "[BOJ] 1342 행운의 문자열 with Python"
date: "2022-03-01"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "그래프 이론", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1342" target="_blank">BOJ 1342 행운의 문자열</a>

<br>

### 💡 조건

1.  인접해 있는 모든 문자가 같지 않은 문자열을 행운의 문자열이라고 한다고 한다.
2.  준영이는 문자열 S에 나오는 문자를 재배치하면 서로 다른 행운의 문자열이 몇 개 나오는지 궁금해졌다.
3.  만약 원래 문자열 S도 행운의 문자열이라면 그것도 개수에 포함한다.
4.  S의 길이는 최대 10이고, 알파벳 소문자로만 이루어져 있다.
5.  첫째 줄에 위치를 재배치해서 얻은 서로 다른 행운의 문자열의 개수를 출력한다.
6.  **브루트포스 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
abcdefghij
```

#### 실행결과

```py
3628800
```

<br>

### ⌨️ 문제 풀이

1.  브루트포스 알고리즘으로 해결하는 문제였습니다.
2.  arr 에 입력받은 문자열을 저장한 뒤, 순차적으로 순회하면서 point 배열에 점수를 부여합니다.
3.  solve() 함수는 재귀함수입니다.
4.  arr 에 있는 중복되지 않는 문자를 하니씩 넣으면서 만들 수 있는 문자열마다 cnt를 하나씩 늘려줍니다.
5.  cnt를 출력합니다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

arr = stdin.readline().rstrip()
cnt = 0
point = [0 for _ in range(26)]
for i in arr:
    point[ord(i) - 97] += 1


def solve(goal, p):
    global cnt
    if goal == 0:
        cnt += 1
        return

    for c in set(list(arr)):
        if point[ord(c) - 97] > 0 and c != p:
            point[ord(c) - 97] -= 1
            solve(goal - 1, c)
            point[ord(c) - 97] += 1


solve(len(arr), '')
print(cnt)
```

<br>

### 💾 느낀점

1.  재귀함수를 통해서 브루트포스를 구현했습니다.
2.  파이썬에서는 pypy로 채점이 가능했습니다.
3.  시간을 단축할 수 있는 방법을 생각해보는 것도 좋겠습니다.