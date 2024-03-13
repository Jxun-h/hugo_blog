---
author: ["Jxun-h"]
title: "[BOJ] 19941 햄버거 분배 with Python"
date: "2022-02-20"
description: ""
summary: ""
tags: ["자료구조", "PS", "그리디", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/19941" target="_blank">BOJ 19941 햄버거 분배</a>

<br>

### 💡 조건

1.  식탁의 길이가 N이다.  
    사람들(P)은 자신의 위치에서 거리가 K 이하인 햄버거를 먹을 수 있다.  
    1 <= N <= 20,000  
    1 <= K <= 10
2.  햄버거를 먹을 수 있는 사람의 최대 수를 구하는 프로그램을 작성.
3.  **그리디 알고리즘** 유형의 문제

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, k = map(int, stdin.readline().split())
arr = list(stdin.readline().rstrip())
res = 0

for i in range(n):
    if arr[i] == 'P':
        for j in range(i - k, i + k + 1):
            if -1 < j < n:
                if arr[j] == 'H':
                    arr[j] = '-'
                    res += 1
                    break

print(res)
```

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
20 1
HHPHPPHHPPHPPPHPHPHP
```

#### 실행결과

```py
8
```

<br>

### ⌨️ 문제 풀이

1.  식탁의 길이 N과 햄버거를 먹을 수 있는 거리 K 를 입력받는다.
2.  N 길이의 햄버거와 사람의 위치의 정보가 담긴 문자열을 입력받아 arr 리스트에 저장한다.
3.  n 만큼 arr 리스트를 순회하면서 arr[i]가 사람일 때, i - k 부터 i + k + 1 까지 순회한다  
    i번째에 위치한 사람이 i - k 부터 i + k + 1 거리의 햄버거를 먹을 수 있기 때문에.
4.  0 <= j < n 의 조건을 만족하고 arr[j]가 햄버거라면 arr의 해당 번호를 이미 먹은 표시로 - 로 변경하고 res + 1, break

<br>

### 💾 느낀점

1.  그리디는 개념자체로는 이해가 쉬우나 막상 문제를 풀면 머리안에서 꼬여버리는 경우가 많다.
2.  앞으로 그리디를 풀 때는 마음을 내려놓고 천천히 생각해보는 습관을 길러야겠다