---
author: ["Jxun-h"]
title: "[BOJ] 14888 연산자 끼워넣기 with Python"
date: "2022-01-24"
description: ""
summary: ""
tags: ["자료구조", "PS", "순열", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/14888" target="_blank">BOJ 14888 연산자 끼워넣기</a>

<br>

### 💡 조건

1.  N개의 수로 이루어진 수열 A1, A2, ..., AN
2.  수와 수 사이에 끼워넣을 수 있는 N-1개의 연산자  
    연산자는 덧셈(+), 뺄셈(-), 곱셈(×), 나눗셈(÷)으로만 이루어져 있다.
3.  수의 개수 N(2 ≤ N ≤ 11)  
    A1, A2, ..., AN이 주어진다. (1 ≤ Ai ≤ 100)
4.  첫째 줄에 만들 수 있는 식의 결과의 최댓값을, 둘째 줄에는 최솟값을 출력
5.  **순열, 브루트포스 알고리즘 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
2
5 6
0 0 1 0
```

#### 실행결과

```py
30
30
```

<br>

### ⌨️ 문제 풀이

1.  permutations 라이브러리 import
2.  연산자를 덧셈(+), 뺄셈(-), 곱셈(×), 나눗셈(÷) 순서대로 담은 gi 리스트 선언.
3.  연산자의 개수 리스트를 입력받아 각 연산자의 개수만큼 곱하여 cg 리스트에 extend 해준다.
4.  cg 리스트의 길이는 입력받은 수열의 길이 - 1이다.  
    permutaions 함수를 통해 순열을 통해 연산자의 경우를 뽑아 calculation 함수에 넣고 계산한다.
5.  **calculation 함수에서 zero division 에러를 조심해야한다.**
6.  calculation 함수에서 계산한 결과값으로 최솟값과 최댓값을 갱신해준다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from itertools import permutations

n = int(stdin.readline().rstrip())
num = list(map(int, stdin.readline().split()))
cal_ = list(map(int, stdin.readline().split()))


gi = ['+', '-', '*', '/']
cg = []
vmax = -1e9
vmin = 1e9


def calculation(sign, num):
    global vmax, vmin
    calc_num = num[0]

    for idx in range(1, len(num)):
        if sign[idx - 1] == '+':
            calc_num += num[idx]

        elif sign[idx - 1] == '-':
            calc_num -= num[idx]

        elif sign[idx - 1] == '*':
            calc_num *= num[idx]

        elif sign[idx - 1] == '/':
            if num[idx] < 0 or calc_num < 0:
                calc_num = abs(calc_num) // abs(num[idx]) * -1
            else:
                calc_num //= num[idx]

    vmax = max(vmax, calc_num)
    vmin = min(vmin, calc_num)


for i in range(4):
    cg.extend([gi[i]] * cal_[i])


for sign in list(set(permutations(cg, n - 1))):
    calculation(sign, num)

print(vmax)
print(vmin)
```

<br>

### 💾 느낀점

1.  permutations 함수를 사용하여 간단하게 풀 수 있어 매우 착한 문제였다고 생각합니다.
2.  시간초과가 안나게 하기 위해서 permutations 함수 결과를 set() 으로 둘러싸서 중복을 제거했습니다.