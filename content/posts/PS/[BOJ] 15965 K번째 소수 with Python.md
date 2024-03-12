---
author: ["Jxun-h"]
title: "[BOJ] 15965 K번째 소수 with Python"
date: "2022-03-04"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "에라토스테네스의 체", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/15965" target="_blank">BOJ 15965 K번째 소수</a>

<br>

### 💡 조건

1.  서브태스크가 존재한다.
2.  2 이상의 자연수 N이 1과 N을 제외하고 어떤 자연수로도 나누어 떨어지지 않을 때 소수라고 한다.
3.  자연수 K가 주어진다.(1 ≤ K ≤ 500,000)
4.  k번째 소수를 구하는 문제
5.  **수학, 에라토스테네스의 체** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3
```

#### 실행결과

```py
5
```

<br>

### ⌨️ 문제 풀이

1.  에라토스테네스의 체를 사용하여 풀이를 하면 됩니다.
2.  **i 가 소수일 때, i의 배수는 소수가 아니다** 라는 아이디어에서 시작을 합니다.
3.  i가 소수로 판별이 되었다면, 10^7 까지 검사를 하면서 i의 배수는 모두 array 배열에서 0으로 체크합니다.
4.  소수로 판별된 i는 answer에 추가해줍니다.

<br>

### 🖥 소스 코드

```py
BIG_NUM = 10**7

k = int(input())
array = [1 for _ in range(BIG_NUM + 1)]

answer = []
for i in range(2, BIG_NUM + 1):
    if array[i]:
        answer.append(i)
        for j in range(i+i, BIG_NUM + 1, i):
            array[j] = 0

print(answer[k - 1])
```

<br>

### 💾 느낀점

1.  에라토스테네스의 체가 익숙하지 않은 상태에서 풀었었던 문제였다.
2.  지금은 문제를 슥 읽으니 바로 풀이가 생각이 났다.