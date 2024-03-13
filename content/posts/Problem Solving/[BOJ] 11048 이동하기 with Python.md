---
author: ["Jxun-h"]
title: "[BOJ] 11048 이동하기 with Python"
date: "2022-02-19"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/11048" target="_blank">BOJ 11048 이동하기</a>

<br>

### 💡 조건

1.  N×M 크기의 미로 (1 ≤ N, M ≤ 1,000)
2.  (r, c)에 있으면, (r+1, c), (r, c+1), (r+1, c+1)로 이동가능.
3.  준규가 (N, M)으로 이동할 때, 가져올 수 있는 사탕 개수의 최댓값을 구하는 문제
4.  N개 줄에는 총 M개의 숫자가 주어지며, r번째 줄의 c번째 수는 (r, c)에 놓여져 있는 사탕의 개수이다.
5.  사탕의 개수는 0보다 크거나 같고, 100보다 작거나 같다.
6.  **다이나믹프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4 3
1 2 3
6 5 4
7 8 9
12 11 10
```

#### 실행결과

```py
47
```

<br>

### ⌨️ 문제 풀이

1.  다이나믹 프로그래밍 유형의 문제입니다. 준규가 이동하면서 사탕을 모두 가져갈 수 있습니다.
2.  arr 리스트에 각 사탕이 놓여져 있는 숫자를 입력받습니다.
3.  candy 리스트는 준규가 챙긴 숫자의 최댓값을 저장할 리스트 입니다.
4.  candy[0][0] 은 arr[0][0] 이 되겠습니다.  
    왜냐하면 준규는 (1, 1)에 위치하고 있기 때문입니다.
5.  1부터 각각 n, m 만큼 이중 반복문으로 순회해줍니다.  
    candy[i][j] 의 숫자를 최댓값으로 갱신합니다.
6.  준규가 움직일 수 있는 방향은 (0, 1), (1, 0), (1, 1) 이며  
    이동 방향에 따라서 최댓값을 선택해서 candy를 갱신하고 (n - 1, m - 1) 인덱스에 있는 값을 출력합니다.


<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = map(int, stdin.readline().split())
arr = []
candy = [[0] * m for _ in range(n)]
res = 0

for _ in range(n):
    arr.append(list(map(int, stdin.readline().split())))

candy[0][0] = arr[0][0]

for i in range(1, m):
    candy[0][i] = arr[0][i] + candy[0][i - 1]

for i in range(1, n):
    candy[i][0] = arr[i][0] + candy[i - 1][0]


for i in range(1, n):
    for j in range(1, m):
        candy[i][j] = max(candy[i - 1][j], candy[i][j - 1], candy[i - 1][j - 1]) + arr[i][j]

print(candy[n - 1][m - 1])
```

<br>

### 💾 느낀점

1.  실버 수준의 다이나믹프로그래밍 유형의 문제였는데, 이 유형을 풀어본 적이 있다면 풀 수 있는 문제였습니다.
2.  그리디 문제도 이런 문제가 비슷하게 있는데, 입력받은 N과 M의 값을 보고 쎄한 느낌을 느끼고 그리디가 아닐 것이라는 생각을 했습니다.
3.  점화식을 짜는게 아직 어렵습니다.