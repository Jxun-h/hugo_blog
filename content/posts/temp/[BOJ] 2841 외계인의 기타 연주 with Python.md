---
author: ["Jxun-h"]
title: "[BOJ] 2841 외계인의 기타 연주 with Python"
date: "2021-12-01"
description: ""
summary: ""
tags: ["자료구조", "PS", "스택", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2841" target="_blank">BOJ 2841 외계인의 기타 연주</a>

<br>

### 💡 조건

1.  멜로디는 음의 연속이고, 각 음은 줄에서 해당하는 프렛을 누르고 줄을 튕기면 연주할 수 있다.
2.  어떤 줄의 프렛을 여러 개 누르고 있다면, 가장 높은 프렛의 음이 발생.
3.  멜로디에 포함되어 있는 음의 수 `N`과 한 줄에 있는 프렛의 수 `P`가 주어진다. `(N ≤ 500,000, 2 ≤ P ≤ 300,000)`
4.  2번 프렛의 음을 연주하려고 한다면, 5번과 7번을 누르던 손가락을 뗀 다음에 2번 프렛을 누르고 연주해야 한다.
5.  손가락의 가장 적게 움직이는 회수를 구하는 프로그램을 작성.
6.  **Stack, 자료구조 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
7 15
1 5
2 3
2 5
2 7
2 4
1 5
1 3
```

#### 실행결과

```python
9
```

### ⌨️ 문제 풀이

1.  기타의 줄을 의미하는 stack 2차원 리스트를 생성한다.  
    스택의 각 원소에 해당하는 리스트에는 누르고 있는 프렛 숫자 데이터가 저장된다.
2.  입력을 받으면서, 프렛 숫자를 각 줄에 해당하는 리스트에 저장한다.
3.  입력받은 줄에 해당하는 리스트에 이미 누르고 있는 프렛에 해당하는 데이터가 있다면,  
    입력받은 프렛 번호가 이미 누르고 있는 프렛의 번호보다 작아질 때까지 pop()을 해주면서 res += 1을 해준다.  
    만약 pop() 을 할 필요가 없다면 바로 추가해준다.
4.  프렛의 번호가 겹치면 더 해당 줄에 프렛 번호를 추가하지 않고, 겹치지 않는다면 추가하고, res += 1을 해준다.
5.  n만큼 반복했다면, res 를 출력한다.

<br>

### 🖥 소스 코드

```python
from sys import stdin
import heapq

n, p = map(int, stdin.readline().split())
stack = [[] for _ in range(7)]
res = 0

for _ in range(n):
    j, f = map(int, stdin.readline().split())

    if not stack[j]:
        heapq.heappush(stack[j], f)
        res += 1

    elif stack[j][-1] < f:
        heapq.heappush(stack[j], f)
        res += 1

    elif stack[j][-1] > f:
        while 1:
            if not stack[j]:
                res += 1
                stack[j].append(f)
                break
            if stack[j][-1] <= f:
                if stack[j][-1] < f:
                    heapq.heappush(stack[j], f)
                    res += 1
                break
            stack[j].pop()
            res += 1

print(res)
```

<br>

### 💾 느낀점

1.  stack 자료구조를 활요하는 문제였다.
2.  아이디어를 떠올리기까지 시간이 꽤 걸린 문제였다.
3.  stack 의 개념을 알면, 이를 다양한 방면으로 활용할 수 있다는 것을 알게 해주었다.
4.  자료구조 문제는 좋은 아이디어를 떠올릴 수 있게 많이 풀어봐야겠다.