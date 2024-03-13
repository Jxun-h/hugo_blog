---
author: ["Jxun-h"]
title: "[BOJ] 1057 토너먼트 with Python"
date: "2022-06-05"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1057" target="_blank">BOJ 1057 토너먼트</a>

<br>

### 💡 조건

1.  N명의 참가자는 번호가 1번부터 N번까지 배정받는다.  
    그러고 난 후에 서로 인접한 번호끼리 스타를 한다. 이긴 사람은 다음 라운드에 진출하고, 진 사람은 그 라운드에서 떨어진다.

2.  그 라운드의 참가자가 홀수명이라면, 마지막 번호를 가진 참가자는 다음 라운드로 자동 진출한다. 다음 라운드에선 다시 참가자의 번호를 1번부터 매긴다.

3.  번호를 매기는 순서는 처음 번호의 순서를 유지하면서 1번부터 매긴다.  
    이 말은 1번과 2번이 스타를 해서 1번이 진출하고, 3번과 4번이 스타를 해서 4번이 진출했다면, 4번은 다음 라운드에서 번호 2번을 배정받는다.  
    번호를 다시 배정받은 후에 한 명만 남을 때까지 라운드를 계속 한다.

4.  일단 김지민과 임한수는 서로 대결하기 전까지 항상 이긴다고 가정한다.  
    1 라운드에서 김지민의 번호와 임한수의 번호가 주어질 때, 과연 김지민과 임한수가 몇 라운드에서 대결하는지 출력하는 문제

5.  참가자의 수 N과 1 라운드에서 김지민의 번호와 임한수의 번호가 순서대로 주어진다.  
    N은 2보다 크거나 같고, 100,000보다 작거나 같은 자연수이고, 김지민의 번호와 임한수의 번호는 N보다 작거나 같은 자연수이고, 서로 다르다.  
    첫째 줄에 김지민과 임한수가 대결하는 라운드 번호를 출력한다. 만약 서로 대결하지 않을 때는 -1을 출력한다.

6.  **브루트포스 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
65536 1000 35000
```

#### 실행결과

```py
16
```

<br>

### ⌨️ 문제 풀이

1.  총 참가자의 수만큼 team list 를 만든다. 이 리스트에 김지민과 임한수의 번호를 표시한다.

2.  solve 함수에서 김지민과 임한수일 때 temp 리스트에 1을 추가하고 아닌 경우, 0을 추가한다.

3.  부전승인 경우, 맨 마지막 인원을 temp에 추가한다.

4.  점점 반으로 줄어드는 팀을 재귀로 구현해서 순회한다.

5.  team 리스트의 값이 둘 다 1 이면 라운드를 return한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin, setrecursionlimit

setrecursionlimit(10 ** 6)

data = list(map(int, stdin.readline().split()))
team = [0 for _ in range(1, data[0] + 1)]
for i in data[1:]:
    team[i - 1] = 1


def solve(round, length):
    global team
    temp = []
    for i in range(0, length // 2 * 2, 2):
        t1, t2 = i, i + 1
        if team[t1] and team[t2]:
            return round
        elif team[t1] or team[t2]:
            temp.append(1)
        else:
            temp.append(0)

    if length % 2 != 0:
        temp.append(team[-1])

    team = temp[:]

    if length % 2 != 0:
        return solve(round + 1, length // 2 + 1)
    else:
        return solve(round + 1, length // 2)


print(solve(1, data[0]))
```
