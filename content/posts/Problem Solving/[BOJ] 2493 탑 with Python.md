---
author: ["Jxun-h"]
title: "[BOJ] 2493 탑 with Python"
date: "2022-03-14"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2493" target="_blank">BOJ 2493 탑</a>

<br>

### 💡 조건

1.  일직선 위에 N개의 높이가 서로 다른 탑을 수평 직선의 왼쪽부터 오른쪽 방향으로 차례로 세우고, 각 탑의 꼭대기에 레이저 송신기를 설치하였다.
2.  모든 탑의 레이저 송신기는 레이저 신호를 지표면과 평행하게 **수평 직선의 왼쪽 방향으로 발사**하고,  
    탑의 기둥 모두에는 레이저 신호를 수신하는 장치가 설치되어 있다.  
    **하나의 탑에서 발사된 레이저 신호는 가장 먼저 만나는 단 하나의 탑에서만 수신이 가능**하다.
3.  N과 탑들의 높이가 주어질 때, 각각의 탑에서 발사한 레이저 신호를 어느 탑에서 수신하는지를 알아내는 문제.
4.  N은 1 이상 500,000 이하
5.  탑들의 높이는 1 이상 100,000,000 이하의 정수
6.  **다이나믹프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5
6 9 5 7 4
```

#### 실행결과

```py
0 0 2 2 4
```

<br>

### ⌨️ 문제 풀이

1.  n의 길이의 data를 차례대로 순회한다.
2.  stack이 빌 때까지 while 문을 통해서 반복하며
3.  stack 맨 마지막 탑이 현재 검사하는 탑보다 값이 크면 현재 검사하는 탑은 스택 맨 마지막 탑이 신호를 받고 있다는 뜻.  
    ans[i] 의 값을 stack의 [-1][0] 에서 1을 더해 넣어주고 while 반복문을 정지.
4.  (3)번의 조건에 해당하지 않는다면 stack 맨 마지막 값을 뺀다.
5.  while 문이 끝나면 stack에 (i, data[i])를 넣어주고 다시 n 만큼 순회하는 반복문을 이어 진행한다.
6.  ans의 내용을 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
data = list(map(int, stdin.readline().split()))
stack = []
ans = [0 for _ in range(n)]

for i in range(n):
    while stack:
        if stack[-1][1] > data[i]:
            ans[i] = stack[-1][0] + 1
            break

        else:
            stack.pop()

    stack.append((i, data[i]))

print(*ans)
```

<br>

### 💾 느낀점

1.  스택을 사용하여 푸는 문제라고 생각을 하지 못했다.
2.  왜 스택을 하용하는지 디버깅 하기 전까지는 이해를 못했었다.
3.  스택의 사용 방법이 더 많다는 것을 느꼈으며, 스택에 대한 문제를 한번 더 풀어봐야겠다.