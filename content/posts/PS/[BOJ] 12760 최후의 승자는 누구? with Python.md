---
author: ["Jxun-h"]
title: "[BOJ] 12760 최후의 승자는 누구? with Python"
date: "2022-03-10"
description: ""
summary: ""
tags: ["자료구조", "PS", "정렬", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/12760" target="_blank">BOJ 12760 최후의 승자는 누구?</a>

<br>

### 💡 조건

1.  최종 플레이어 N명이 남아있다. 각 플레이어는 M장씩의 숫자가 적힌 카드를 가지고 있으며,  
    이들은 매 턴 자신이 가진 카드 중 가장 큰 카드를 두고 비교를 하는데, 그 카드들 중 가장 큰 수를 가진 플레이어가 1점을 획득한다.
2.  그 턴에 사용된 카드는 버리기로 한다. (가장 큰 수를 가진 플레이어는 여러 명일 수 있다.)

3. M번의 경기 후 가장 많은 점수를 획득한 플레이어는 몇 번 플레이어인지 구하는 문제.

4.  2 <= N <= 100, 1 <= M <= 100  
    1 <= 카드에 적힌 숫자 <= 100
5.  가장 많은 점수를 획득한 플레이어가 여러 명일 경우, 빈칸을 사이에 두고 플레이어들의 번호를 오름차순으로 출력한다.
6.  **정렬** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5 3
5 4 3
3 4 5
3 5 4
4 5 3
3 4 4
```

#### 실행결과

```py
1 2 3 4
```

<br>

### ⌨️ 문제 풀이

1.  d 변수는 dictionary 이며, 각 플레이어의 점수를 저장할 변수이다.
2.  N 명의 플레이어가 각자 들고 있는 카드의 숫자들이 입력될 때, 그 숫자들을 내림차순으로 정렬하여 players에 넣어준다.
3.  각 플레이어의 카드를 순회하면서 가장 큰 카드 값을 저장한다.
4.  각 플레이어의 카드를 순회하면서 mx[j] 가 i 번 플레이어의[j]번째 카드와 값이 같다면, d[i + 1] 에 + 1을 해준다.
5.  d 에 저장된 값 중, 가장 큰 값을 골라낸 뒤, mx_cnt 에 저장한다.
6.  d를 순회하면서 mx_cnt 와 같은 값을 가진 키를 res에 저장해준다.  
    res를 출력할 땐, 오름차순 정렬을 한 번 수행해준 뒤 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = map(int, stdin.readline().split())
d = {x: 0 for x in range(1, n + 1)}
players = []
for i in range(n):
    cards = list(map(int, stdin.readline().split()))
    cards.sort()
    players.append(list(reversed(cards)))

mx = [0 for _ in range(m)]

for i in range(n):
    for j in range(m):
        mx[j] = max(mx[j], players[i][j])

for i in range(n):
    for j in range(m):
        if mx[j] == players[i][j]:
            d[i + 1] += 1

mx_cnt = max(d.values())
res = []
for key, item in d.items():
    if item == mx_cnt:
        res.append(key)
res.sort()
print(*res)
```

<br>

### 💾 느낀점

1.  간단하게 풀 수 있었던 정렬 문제였습니다.
2.  카드의 숫자를 큰 순서대로 보아야하는 것을 떠올리지 못해 조금 헤맸습니다.