---
author: ["Jxun-h"]
title: "[BOJ] 2631 줄세우기 with Python"
date: "2022-03-18"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2631" target="_blank">BOJ 2631 줄세우기</a>

<br>

### 💡 조건

1.  선생님은 1번부터 N번까지 번호가 적혀있는 번호표를 아이들의 가슴에 붙여주었다.
2.  선생님은 아이들을 효과적으로 보호하기 위해 목적지까지 번호순서대로 일렬로 서서 걸어가도록 하였다.
3.  이동 도중에 보니 아이들의 번호순서가 바뀌어 다시 번호 순서대로 줄을 세우기 위해서 아이들의 위치를 옮기려고 한다.
4.  아이들이 혼란스러워하지 않도록 하기 위해 위치를 옮기는 아이들의 수를 최소로 하려고 한다.
5.  아이들의 수 N은 2 이상 200 이하의 정수이다.
6.  **다이나믹프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
7
3
7
5
2
6
1
4
```

#### 실행결과

```py
4
```

<br>

### ⌨️ 문제 풀이

1.  가장 긴 증가하는 부분 수열 알고리즘으로 해결 할 수 있는 문제입니다.
2.  입력받은 아이들의 순서를 유지하고 숫자를 뽑았을 때, 증가하는 수열인데 가장 긴 길이를 구하는 알고리즘입니다.
3.  N만큼 순회하면서 i번째 아이를 이전의 아이의 번호를 i-1번째 아이의 숫자와 비교해  
    dp[i] 번째 아이의 번호와 dp[j]+1 의 숫자 중 큰걸 dp[i]에 dp 리스트를 갱신합니다.
4.  dp 리스트에서 가장 큰 값을 찾아 답을 출력할 변수 lis와 max() 함수로 크기를 비교한 후 저장합니다.
5.  answer 변수에 n명의 아이 - lis 값을 저장하고 출력합니다.
6.  n명의 아이 중, 이동하는 아이의 수는 lis 입니다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
num = [int(stdin.readline()) for _ in range(n)]

dp = [0 for _ in range(n)]

for i in range(n):
    dp[i] = 1
    for j in range(i):
        if num[i] > num[j]:
            dp[i] = max(dp[i], dp[j] + 1)

lis = 0
lis = max(lis, max(dp))

answer = n - lis
print(answer)
```

<br>

### 💾 느낀점

1.  다이나믹프로그래밍은 진짜 극혐이다.