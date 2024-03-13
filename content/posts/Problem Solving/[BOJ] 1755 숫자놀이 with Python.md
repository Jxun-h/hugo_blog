---
author: ["Jxun-h"]
title: "[BOJ] 1755 숫자놀이 with Python"
date: "2022-03-06"
description: ""
summary: ""
tags: ["자료구조", "PS", "정렬", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1755" target="_blank">BOJ 1755 숫자놀이</a>

<br>

### 💡 조건

1.  79를 영어로 읽되 숫자 단위로 하나씩 읽는다면 "seven nine"이 된다. 80은 마찬가지로 "eight zero"라고 읽는다.
2.  79는 80보다 작지만, 영어로 숫자 하나씩 읽는다면 "eight zero"가 "seven nine"보다 사전순으로 먼저 온다.
3.  문제는 정수 M, N(1 ≤ M ≤ N ≤ 99)이 주어지면 M 이상 N 이하의 정수를 숫자 하나씩 읽었을 때를 기준으로 사전순으로 정렬하여 출력하는 것.
4.  M 이상 N 이하의 정수를 문제 조건에 맞게 정렬하여 한 줄에 10개씩 출력한다.
5.  **정렬** 유형의 문제

### 🔖 예제 및 실행결과

#### 예제

```py
8 28
```

#### 실행결과

```py
8 9 18 15 14 19 11 17 16 13
12 10 28 25 24 21 27 26 23 22
20
```

<br>

### ⌨️ 문제 풀이

1.  dict 형 변수 d 에 각 숫자마다의 영어 문자열을 저장한다.
2.  n부터 m + 1 까지 순회(i)하면서 i를 문자열로 변환했을 때 길이만큼 또 순회(j)한다.
3.  s 배열에 data[j]를 영어 문자열로 변환 후 넣어준다.
4.  j 순회가 끝나면 s 리스트에 i를 문자열로 변환한 값을 추가해준다.
5.  그 후, temp 배열에 s를 튜플로 만들어 추가한다.
6.  temp를 정렬하고, 정렬된 숫자값을 10개씩 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
arr = []
num = 0
i = 1

while n > num:
    num += (i * (i + 1)) // 2
    arr.append(num)
    i += 1

dp = [int(1e9) for i in range(n + 1)]
for i in range(1, n + 1):
    for num in arr:
        if num == i:
            dp[i] = 1
            break
        elif num > i:
            break
        dp[i] = min(dp[i], 1 + dp[i - num])

print(dp[n])
```

<br>

### 💾 느낀점

1.  그다지 어려운 문제가 아니었는데, 복잡하게 생각해서 힘들었던 문제였습니다.