---
author: ["Jxun-h"]
title: "[BOJ] 12788 제 2회 IUPC는 잘 개최될 수 있을까? with Python"
date: "2022-03-16"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/12788" target="_blank">BOJ 12788 제 2회 IUPC는 잘 개최될 수 있을까?</a>

<br>

### 💡 조건

1.  대회 개최를 위한 예산을 아끼기 위하여 펜을 구매하지 않고 CTP회원들에게 펜을 빌리기로 하였다.
2.  CTP에는 N명의 회원들이 존재하며 각각의 회원들의 필통에 들어있는 펜의 개수는 모두 다르다.  
    정은이는 여러명의 회원에게 펜을 빌릴경우 펜을 돌려주기에 번거롭다고 생각하여 **최소한의 회원들에게 펜을 빌려 참가자들에게 나누어 주려고 한다.**
3.  대회에 참가하는 참가자들은 팀을 구성해서 참가하는데 모든 팀원에게 펜을 지급해야한다.
4.  한 팀이 k명의 팀원으로 구성되어 있을때 몇 명의 회원들에게 펜을 빌려야하는지 출력하는 문제.
5.  CTP의 회원수 N(1 ≤ N ≤ 1,000)  
    대회에 참가한 팀의 수 M(1 ≤ M ≤ 1,000)  
    팀을 구성하는데 필요한 팀원의 수 K(1 ≤ K ≤ 10)  
    각각의 CTP 회원들이 가지고 있는 펜의 수 A(0 ≤ A ≤ 100)
6.  **다이나믹프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
7
36 3
9 70 15 13 19 20 11
```

#### 실행결과

```py
3
```

<br>

### ⌨️ 문제 풀이

1.  입력 받은 배열을 정렬한 뒤, n크기의 배열을 순회한다.
2.  필요한 펜의 수(m * k)에서 arr[i] 를 뺀 결과가 만약
    -   -1보다 크다면, cnt + 1, need_pens - arr[i]
    -   0보다 작다면, cnt + 1, need_pens - arr[i]
3.  need_pensrk > 0 일 경우, STRESS를 출력하고 그 반대의 경우 cnt를 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
m, k = map(int, stdin.readline().split())
arr = list(map(int, stdin.readline().split()))
arr.sort(reverse=True)

need_pens = m * k

cnt = 0
for i in range(n):
    if need_pens == 0:
        break

    if need_pens - arr[i] > -1:
        cnt += 1
        need_pens -= arr[i]

    elif need_pens - arr[i] < 0:
        cnt += 1
        need_pens -= arr[i]
        break

print("STRESS") if need_pens > 0 else print(cnt)
```

<br>

### 💾 느낀점