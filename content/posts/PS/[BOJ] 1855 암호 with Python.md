---
author: ["Jxun-h"]
title: "[BOJ] 1855 암호 with Python"
date: "2022-03-01"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "문자열", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1855" target="_blank">BOJ 1855 암호</a>

<br>

### 💡 조건

1.  먼저 암호화 할 문자열을 1,1부터 위에서 아래 순서대로 채운다. 그리고 가장 밑의 행을 채운 후에는 오른쪽 열에서 다시 같은 과정을 반복한다.
2.  암호화 된 문자열과 몇 개의 열로 암호화를 하였는지 주어져 있을 때 원래의 문자열을 구하는 프로그램을 작성하는 문제.
3.  열의 개수 K(1 ≤ K ≤ 20)가 주어진다.  
    두 번째 줄에는 암호화 된 문자열(모두 영소문자)이 주어진다.
4.  (문자열의 길이는 200 이하이며 K의 배수이다.)
5.  **구현, 문자열** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3
aeijfbcgklhd
```

#### 실행결과

```py
abcdefghijkl
```

<br>

### ⌨️ 문제 풀이

1.  열의 개수와 문자열을 입력받고, 열의 개수에 맞게 문자열을 쪼개서 arr 리스트에 저장한다.
2.  arr의 행의 개수만큼 순회하면서 i를 2로 나누었을 때, 0인 경우 arr[i] 을 뒤집어 arr에 다시 저장한다.
3.  결과값을 담을 res 변수에 arr 배열을 차례대로 순회하면서 res에 문자열을 추가해준다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
s = stdin.readline().rstrip()
arr = []
for i in range(0, len(s), n):
    arr.append(list(s[i:i+n]))

for i in range(len(arr)):
    if i % 2 != 0:
        data = list(reversed(arr[i]))
        arr[i] = data

res = ''
for j in range(n):
    for i in range(len(arr)):
        res += arr[i][j]
print(res)
```

<br>

### 💾 느낀점

1.  친절하고 재미있는 문자열 + 구현 문제였습니다.