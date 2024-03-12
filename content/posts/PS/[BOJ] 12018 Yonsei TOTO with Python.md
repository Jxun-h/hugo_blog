---
author: ["Jxun-h"]
title: "[BOJ] 12018 Yonsei TOTO with Python"
date: "2022-03-09"
description: ""
summary: ""
tags: ["자료구조", "PS", "정렬", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/12018" target="_blank">BOJ 12018 Yonsei TOTO</a>

<br>

### 💡 조건

1.  각각의 학생들에게 마일리지를 주어 듣고 싶은 과목에 마일리지를 과목당 1~36을 분배한다.  
    그리고 모두 분배가 끝이 나면 과목에 대해서 마일리지를 많이 투자한 순으로 그 과목의 수강인원만큼 신청되는 방식이다.
2.  성준이는 주어진 마일리지로 최대한 많은 과목을 신청하고 싶어 한다.  
    (내가 마일리지를 넣고 이후에 과목을 신청하는 사람은 없다) 마일리지는 한 과목에 1에서 36까지 넣을 수 있다.
3.  과목 수 n (1 ≤ n ≤ 100)  
    마일리지 m (1 ≤ m ≤ 100)  
    각 과목마다 2줄의 입력이 주어지는데 첫째 줄에는 각 과목에 신청한 사람 수 Pi과 과목의 수강인원 Li  
    그 다음 줄에는 각 사람이 마일리지를 얼마나 넣었는지 주어진다.
4.  **정렬** 유형의 문제

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = map(int, stdin.readline().split())
res = 0
c = []

for i in range(n):
    p, l = map(int, stdin.readline().split())
    point = list(map(int, stdin.readline().split()))
    point.sort(reverse=True)
    if p < l:
        c.append(1)
    else:
        mile = point[l - 1]
        c.append(mile)

c.sort()
for class_m in c:
    if m - class_m >= 0:
        res += 1
        m -= class_m
print(res)
```

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5 76
5 4 
36 25 1 36 36
4 4
30 24 25 20
6 4
36 36 36 36 36 36
2 4
3 7
5 4
27 15 26 8 14
```

#### 실행결과

```py
4
```

<br>

### ⌨️ 문제 풀이

1.  과목에 신청한 인원 수보다 수강 인원이 높다면, 마일리지를 크게 투자하지 않아도 된다.  
    반대로 신청한 인원 수가 수강 인원보다 높다면, **성준이가 우선순위를 가지기 때문에**  
    **(수강인원) 번째 신청한 사람만큼만 신청하면 수강할 수 있다.**  
    신청한 마일리지는 내림차순으로 정렬해서 계산한다.
2.  `if p < l: c.append(1) else: mile = point[l - 1] c.append(mile)`
3.  c를 정렬하고 성준이가 가지고 있는 마일리지에서 신청할 때 필요한 마일리지를 빼주며, 음수가 되지 않으면 res 에 1을 추가한다

<br>

### 💾 느낀점

1.  그리디가 묻은 정렬을 이용한 문제였습니다.