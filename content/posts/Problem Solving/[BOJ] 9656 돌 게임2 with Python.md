---
author: ["Jxun-h"]
title: "[BOJ] 9656 돌 게임2 with Python"
date: "2023-04-04 17:31:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/9656" target="_blank">BOJ 9656 돌 게임2</a>

<br>

### 💡 조건

1.  탁자 위에 돌 N개가 있다. 상근이와 창영이는 턴을 번갈아가면서 돌을 가져가며, 돌은 1개 또는 3개 가져갈 수 있다.
2.  마지막 돌을 가져가는 사람이 게임을 지게 된다.
3.  두 사람이 **완벽하게 게임을 했을 때**, 이기는 사람을 구하는 문제.
4.  게임은 상근이가 먼저 시작한다.
5.  첫째 줄에 N이 주어진다. (1 ≤ N ≤ 1000)  
    상근이가 게임을 이기면 SK를, 창영이가 게임을 이기면 CY을 출력한다.
6.  **다이나믹 프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
4
```

#### 실행결과 1

```py
SK
```

<br>

### ⌨️ 문제 풀이

1.  [BOJ 9655 돌 게임](https://www.acmicpc.net/problem/9655) 의 문제 풀이와 매우 비슷하다.
2.  [9655 돌 게임 문제 풀이](https://jxun-h.github.io/posts/problem-solving/boj-9655-%EB%8F%8C-%EA%B2%8C%EC%9E%84-with-python/) 를 참고하여 아이디어를 얻어보자.

<br>

### 🖥 소스 코드

```py
from sys import stdin

print('SK' if int(stdin.readline()) % 2 == 0 else 'CY')
```