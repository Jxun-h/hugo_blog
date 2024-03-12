---
author: ["Jxun-h"]
title: "[BOJ] 2628 종이 자르기 with Python"
date: "2022-02-22"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "정수론", "유클리드 호제법", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2628" target="_blank">BOJ 2628 종이 자르기</a>

<br>

### 💡 조건

1.  종이의 가로와 세로의 길이가 차례로 자연수로 주어진다. 가로와 세로의 길이는 최대 100㎝이다.
2.  칼로 잘라야하는 점선의 개수가 주어진다.  
    셋째 줄부터 마지막 줄까지 한 줄에 점선이 하나씩 아래와 같은 방법으로 입력된다.  
    가로로 자르는 점선은 0과 점선 번호가 차례로 주어지고, 세로로 자르는 점선은 1과 점선 번호가 주어진다.
3.  점선을 따라 이 종이를 칼로 자르려고 한다.  
    가로 점선을 따라 자르는 경우는 종이의 왼쪽 끝에서 오른쪽 끝까지, 세로 점선인 경우는 위쪽 끝에서 아래쪽 끝까지 한 번에 자른다.
4.  가장 큰 종이 조각의 넓이가 몇 ㎠인지를 구하는 프로그램
5.  **정렬** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
10 8
3
0 3
1 4
0 2
```

#### 실행결과

```py
30
```

<br>

### ⌨️ 문제 풀이

1.  가로와 세로 처음의 길이를 ga, se 리스트에 각각 넣은 후 시작한다.
2.  가로인 경우와 세로인 경우를 나누어 각각의 리스트에 담는다.
3.  담긴 가로, 세로 리스트를 정렬합니다. max_x, max_y 값을 정렬된 리스트의 가장 첫번째 값으로 초기화 합니다.
4.  정렬된 가로, 세로 리스트를 순회하면서 잘린 종이의 크기가 가장 큰 값을 찾습니다.  
    ga[i + 1] - ga[i] 의 값이 더 크다면 갱신합니다.  
    se[i + 1] - se[i] 의 값이 더 크다면 갱신합니다.
5.  ga * se 의 값을 출력합니다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = map(int, stdin.readline().split())
ga, se = [n], [m]

for i in range(int(stdin.readline())):
    sep, line = map(int, stdin.readline().split())
    if sep == 1:
        ga.append(line)
    else:
        se.append(line)

ga.sort()
se.sort()

max_x, max_y = ga[0], se[0]
for x in range(len(ga)-1):
    max_x = max(max_x, ga[x + 1] - ga[x])

for y in range(len(se)-1):
    max_y = max(max_y, se[y + 1] - se[y])

print(max_x * max_y)
```

<br>

### 💾 느낀점

1.  잘린 종이의 크기를 어떻게 구할지 고민을 했습니다.
2.  가로세로 리스트에 자르기 전의 종이 크기를 넣는 아이디어를 떠올리지 못했습니다.