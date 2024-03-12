---
author: ["Jxun-h"]
title: "[BOJ] 1292 쉽게 푸는 문제 with Python"
date: "2022-02-03"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "수학", "구현", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1292" target="_blank">BOJ 1292 쉽게 푸는 문제</a>

<br>

### 💡 조건

1.  1을 한 번, 2를 두 번, 3을 세 번, 이런 식으로 1 2 2 3 3 3 4 4 4 4 5 .. 이러한 수열을 만들고  
    어느 일정한 구간을 주면 그 구간의 합을 구하는 문제
2.  정수 A, B(1 ≤ A ≤ B ≤ 1,000)가 주어진다.  
    수열에서 A번째 숫자부터 B번째 숫자까지 합을 구하면 된다.
3.  **다이나믹 프로그래밍, 수학, 구현**유형의 문제

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

1.  리스트에 구간합에 대해 값을 저장하여 arr\[m\] - arr\[n-1\]을 하여 출력하면 된다.
2.  구간합의 값을 가진 리스트 arr 에서는 arr\[m\] - arr\[n-1\]을 아래와 같이 말할 수 있다.  
    (첫번째부터 m번째 숫자까지의 합) - (첫번째부터 n-1번째 숫자까지의 합)과 같다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = map(int, stdin.readline().split())
arr = [0, 1]

for i in range(2, m + 1):
    for j in range(i):
        arr.append(arr[-1] + i)
print(arr[m] - arr[n - 1])
```

<br>

### 💾 느낀점

1.  문제 제목대로 쉽게 푸는 문제였고, 매우 친절한 구간합 문제였습니다.