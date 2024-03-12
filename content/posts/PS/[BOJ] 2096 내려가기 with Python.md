---
author: ["Jxun-h"]
title: "[BOJ] 2096 내려가기 with Python"
date: "2022-03-12"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2096" target="_blank">BOJ 2096 내려가기</a>

<br>

### 💡 조건

1.  N줄에 0 이상 9 이하의 숫자가 세 개씩 적혀 있다.  
    내려가기 게임을 하고 있는데, 이 게임은 첫 줄에서 시작해서 마지막 줄에서 끝나게 되는 놀이이다.
2.  먼저 처음에 적혀 있는 세 개의 숫자 중에서 하나를 골라서 시작하게 된다.  
    그리고 다음 줄로 내려가는데, 다음 줄로 내려갈 때에는 다음과 같은 제약 조건이 있다.  
    바로 아래의 수로 넘어가거나, 아니면 바로 아래의 수와 붙어 있는 수로만 이동할 수 있다는 것이다.
3.  최대 점수, 최소 점수를 구하는 프로그램을 작성하는 문제
4.  첫째 줄에 N(1 ≤ N ≤ 100,000)이 주어진다. 다음 N개의 줄에는 숫자가 세 개씩 주어진다.
5.  숫자는 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 중의 하나가 된다.  
    첫째 줄에 얻을 수 있는 최대 점수와 최소 점수를 띄어서 출력한다.
6.  **다이나믹프로그래밍** 유형의 문제

### 🔖 예제 및 실행결과

#### 예제

```py
3
1 2 3
4 5 6
4 9 0
```

#### 실행결과

```py
18 6
```

<br>

### ⌨️ 문제 풀이

1.  입력받은 n만큼 순회한다.
2.  아래층으로 내려가면서 합칠 때 가장 큰 값과 작은 값을 x_temp, n_temp에 저장한다.
3.  dp에 x_temp, n_temp 내용을 저장한다.
4.  최댓갑과 최댓값을 따로 저장할 배열을 만들고, 위치에 따라 선택할 수 있는 값을 달리하여 최댓값과 최솟값을 구하는 것이 목적이다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())

x_dp = [0] * 3
n_dp = [0] * 3

x_temp = [0] * 3
n_temp = [0] * 3

for i in range(n):
    a, b, c = map(int, stdin.readline().split())

    for j in range(3):
        if j == 0:
            x_temp[j] = a + max(x_dp[j], x_dp[j + 1])
            n_temp[j] = a + min(n_dp[j], n_dp[j + 1])

        elif j == 1:
            x_temp[j] = b + max(x_dp[j - 1], x_dp[j], x_dp[j + 1])
            n_temp[j] = b + min(n_dp[j - 1], n_dp[j], n_dp[j + 1])

        elif j == 2:
            x_temp[j] = c + max(x_dp[j], x_dp[j - 1])
            n_temp[j] = c + min(n_dp[j], n_dp[j - 1])

    for j in range(3):
        x_dp[j] = x_temp[j]
        n_dp[j] = n_temp[j]

print(max(x_dp), min(n_dp))
```

<br>

### 💾 느낀점

1.  다이나믹프로그래밍 문제는 역시 점화식 때문에 골치를 많이 썩어하는 것 같다.
2.  생각보다 문제풀이를 보고 어렵지 않았던 문제인데 왜 헤맸을까 하는 생각을 했다.
3.  이러한 유형을 다시 풀었을 때, 잘 풀 수 있게 풀이를 써야겠다는 생각을 했다.