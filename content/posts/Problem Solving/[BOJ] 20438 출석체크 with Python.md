---
author: ["Jxun-h"]
title: "[BOJ] 20438 출석체크 with Python"
date: "2022-06-05"
description: ""
summary: ""
tags: ["자료구조", "PS", "누적합", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/20438" target="_blank">BOJ 20438 출석체크</a>

<br>

### 💡 조건

1.  학생들은 접속 순서대로 3번부터 N + 2번까지 입장 번호를 받게 된다.
2.  지환이가 한 학생에게 출석 코드를 보내게 되면, 해당 학생은 본인의 입장 번호의 배수인 학생들에게 출석 코드를 보내어  
    해당 강의의 출석을 할 수 있게끔 한다. 하지만, K명의 졸고 있는 학생들은 출석 코드를 제출하지 않고, 다른 학생들에게 보내지 않는다.

3.  지환이는 무작위로 한 명의 학생에게 출석 코드를 보내는 행위를 Q번 반복한 뒤,  
    출석부 정리를 위해 특정 구간의 입장 번호를 받은 학생들 중에서 출석이 되지 않은 학생들의 수를 구하고 싶다.

4.  1번째 줄에 학생의 수 N, 졸고 있는 학생의 수 K, 지환이가 출석 코드를 보낼 학생의 수 Q, 주어질 구간의 수 M이 주어진다.  
    (1 ≤ K, Q ≤ N ≤ 5,000, 1 ≤ M ≤ 50,000)

5.  2번째 줄과 3번째 줄에 각각 K명의 졸고 있는 학생의 입장 번호들과 Q명의 출석 코드를 받을 학생의 입장 번호들이 주어진다.

6.  4번째 줄부터 M개의 줄 동안 구간의 범위 S, E가 공백을 사이에 두고 주어진다. (3 ≤ S < E ≤ N + 2)

7.  **누적합, 구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
50 4 5 1
24 15 27 43
3 4 6 20 25
3 52
```

#### 실행결과

```py
25
```

<br>

### ⌨️ 문제 풀이

1.  자는 인원을 먼저 sleep 리스트에 표시해준다.  
    그 후, 해당 구간에 대해 출석체크를 정상적으로 한 인원에 대해서 구간합을 구해준다.

2.  문제에서 요구하는 구간에 대해서 구간의 합을 구해서 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, k, q, m = map(int, stdin.readline().split())
sleep = [0 for _ in range(n + 3)]
check = [0 for _ in range(n + 3)]

for i in map(int, stdin.readline().split()):
    sleep[i] = 1

for i in map(int, stdin.readline().split()):
    if sleep[i]:
        continue

    for j in range(i, n + 3, i):
        if not sleep[j]:
            check[j] = 1

pre = [check[0]]
for i in range(1, n + 3):
    pre.append(pre[-1] + check[i])

for _ in range(m):
    s, e = map(int, stdin.readline().split())
    print(e - s + 1 - pre[e] - pre[s - 1])
```