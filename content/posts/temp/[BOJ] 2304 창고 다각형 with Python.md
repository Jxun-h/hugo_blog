---
author: ["Jxun-h"]
title: "[BOJ] 2304 창고 다각형 with Python"
date: "2021-11-29"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2304" target="_blank">BOJ 2304 창고 다각형</a>

<br>

### 💡 조건

1.  기둥의 개수를 나타내는 정수 `(1 <= N <= 1000)`  
    각 기둥의 왼쪽 면의 위치를 나타내는 정수 `(1 <= L <= 1000)`  
    각 기둥의 높이를 나타내는 정수 `(1 <= H <= 1000)`
2.  **창고 다각형의 면적을 구하는 문제**
3.  모든 기둥이 들어가는 창고를 지으려고 할 때, **지붕이 될 수 있는 조건**은 아래와 같다.
    - 지붕은 수평 부분과 수직 부분으로 구성되며, 모두 연결되어야 한다.
    - 지붕의 수평 부분은 반드시 어떤 기둥의 윗면과 닿아야 한다.
    - 지붕의 수직 부분은 반드시 어떤 기둥의 옆면과 닿아야 한다.
    - 지붕의 가장자리는 땅에 닿아야 한다.
    - 비가 올 때 물이 고이지 않도록 지붕의 어떤 부분도 오목하게 들어간 부분이 없어야 한다.

4.  **자료구조, 브루트포스 알고리즘**유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```
7
2 4
11 4
15 8
4 6
5 3
8 10
13 6
```

#### 실행결과

```
98
```

<br>

### ⌨️ 문제 풀이

1.  간단하게 생각하면 매우 좋은 문제이다. 문제에서 제시된 그림에서도 보이듯, 기둥들 중에서 가장 높이 값이 큰 기둥이 있다.  
    그 가장 높이가 높은 기둥을 중심으로 나누어서 왼쪽에서 오른쪽으로 면적을 구하고, 오른쪽에서 왼쪽으로 면적을 구해 더한 후 출력하면 된다.
2.  index를 잘 구별해서 써야 헷길리지 않을 수 있다.

<br>

### 🖥 소스 코드

```python
from sys import stdin

n = int(stdin.readline())
max_pillar = -1e9
idx = 0
arr = [[] for _ in range(1001)]
res = 0
last_idx = 0

for _ in range(n):
    a, b = map(int, stdin.readline().split())
    if max_pillar < b:
        max_pillar = b
        idx = a

    arr[a].append(b)
    last_idx = max(last_idx, a)

part1 = arr[:idx+1]
part2 = arr[idx+1:last_idx+1]

now = 0
for i in part1:
    if not i:
        res += now
    else:
        if now > i[0]:
            res += now
        else:
            now = i[0]
            res += now

part2.reverse()
now = 0
for i in part2:
    if not i:
        res += now
    else:
        if now > i[0]:
            res += now
        else:
            now = i[0]
            res += now

print(res)
```

<br>

### 💾 느낀점

1.  푼지 조금 오래된 문제이지만, 바로 바자마자 풀이가 생각이 났다.
2.  지금 소스코드를 다시 작성한다면 더 간결하고 이쁘게 구현할 수 있을 것 같다.