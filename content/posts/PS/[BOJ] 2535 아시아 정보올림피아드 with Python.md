---
author: ["Jxun-h"]
title: "[BOJ] 2535 아시아 정보올림피아드 with Python"
date: "2022-02-08"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "정렬", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2535" target="_blank">BOJ 2535 아시아 정보올림피아드</a>

<br>

### 💡 조건

1.  대회참가 학생 수를 나타내는 N, 3 ≤ N ≤ 100.
2.  N개의 줄에는 각 줄마다 한 학생의 소속 국가 번호, 학생 번호, 그리고 성적이 하나의 빈칸을 사이에 두고 주어진다.
3.  국가 번호는 1부터 순서대로 하나의 정수로 주어지며, 각 학생번호는 각 나라별로 1부터 순서대로 하나의 정수로 주어진다.
4.  점수는 0 이상 1000 이하의 정수이고, 동점자는 없다고 가정한다.
5.  **정렬, 구현**유형의 문제.

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
9
1 1 230
1 2 210
1 3 205
2 1 100
2 2 150
3 1 175
3 2 190
3 3 180
3 4 195
```

#### 실행결과

```py
1 1
1 2
3 4
```

<br>

### ⌨️ 문제 풀이

1.  입력을 받아 리스트에 저장할 때, 점수, 참가국, 학생번호 순으로 저장한다.  
    이후, sort 를 해주면 점수순으로 정렬이 된다.
2.  수상을 한 이력을 담을 h 딕셔너리 변수를 하나만들고, 정렬된 grade 리스트를 순회한다.  
    grade 리스트를 순회하면서  
    만약 해당 국가 (grade[i][1])가 수상 이력이 없으면 수상한 국가의 수 cnt + 1  
    수상 이력에 grade[i][1] 를 추가하고 값을 1로 한다.
3.  만약 해당 국가 (grade[i][1])가 수상 이력이 있고, 수상 이력의 수가 2 미만이면 수상한 국가의 수 cnt + 1  
    수상 이력에 해당 국가에 + 1 한다.
4.  만약 수상한 국가가 3이라면 반복문을 멈춘다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
grade = []
for i in range(n):
    a,b,c = map(int, stdin.readline().split())
    grade.append((c, a, b))

h = {}

grade.sort(reverse=True)
cnt = 0
for i in range(n):
    if cnt == 3:
        break

    if grade[i][1] not in h:
        print(*grade[i][1:])
        cnt += 1
        h[grade[i][1]] = 1
    else:
        if h[grade[i][1]] < 2:
            print(*grade[i][1:])
            h[grade[i][1]] += 1
            cnt += 1
        else:
            continue
```

<br>

### 💾 느낀점

1.  정렬을 하고 약간의 조건문만 추가해주면 쉽게 풀 수 있는 문제였습니다.