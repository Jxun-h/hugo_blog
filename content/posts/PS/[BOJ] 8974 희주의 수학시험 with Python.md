---
author: ["Jxun-h"]
title: "[BOJ] 8974 희주의 수학시험 with Python"
date: "2022-03-21"
description: ""
summary: ""
tags: ["자료구조", "PS", "사칙연산", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/8974" target="_blank">BOJ 8974 희주의 수학시험</a>

<br>

### 💡 조건

1.  연습문제 중에 하나가 정수를 적어나가는 것이였는데 수열은 1이 한 개, 2가 두 개, 3이 세 개.. 와 같이 만들어진다.
2.  이제 강민이는 희주에게 두 개의 정수 A, B를 부를텐데, 그럼 희주는 주어진 수열에서 A번째와 B번째 사이에 있는 모든 수들의 합을 말해야한다.
3.  희주에게 문제를 내기 위해 정답을 계산하는 문제
4.  **사칙연산, 구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3 7
```

#### 실행결과

```py
15
```

<br>

### ⌨️ 문제 풀이

1.  반복문을 50회 순회하면서, 각 숫자에 해당하는만큼 리스트에 숫자를 append()한다.
2.  구하고자 하는 범위의 숫자를 순회(i)하면서 arr[i-1] 값을 res에 더해준 뒤, 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

arr, res = [], 0
a, b = map(int, stdin.readline().split())
for i in range(1, 50):
    cnt = 0
    while cnt != i:
        arr.append(i)
        cnt += 1

for i in range(a, b + 1):
    res += arr[i-1]

print(res)
```

<br>

### 💾 느낀점