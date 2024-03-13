---
author: ["Jxun-h"]
title: "[BOJ] 1021 회전하는 큐 with Python"
date: "2022-01-31"
description: ""
summary: ""
tags: ["자료구조", "PS", "큐", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1021" target="_blank">BOJ 1021 회전하는 큐</a>

<br>

### 💡 조건

1.  N개의 원소를 포함하고 있는 양방향 순환 큐
    -   1 <= N <= 50
2.  큐에서 다음과 같은 3가지 연산을 수행할 수 있다.
    -   첫 번째 원소를 뽑아낸다. 이 연산을 수행하면, 원래 큐의 원소가 a1, ..., ak이었던 것이 a2, ..., ak와 같이 된다.
    -   왼쪽으로 한 칸 이동시킨다. 이 연산을 수행하면, a1, ..., ak가 a2, ..., ak, a1이 된다.
    -   오른쪽으로 한 칸 이동시킨다. 이 연산을 수행하면, a1, ..., ak가 ak, a1, ..., ak-1이 된다.
3.  그 원소를 주어진 순서대로 뽑아내는데 드는 2번, 3번 연산의 최솟값을 출력하는 문제.
4.  **Queue, 자료구조 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
32 6
27 16 30 11 6 23
```

#### 실행결과

```py
59
```

<br>

### ⌨️ 문제 풀이

1.  큐의 크기만큼 1부터 N까지의 수를 포함한 리스트를 만들어준다.
2.  결과값을 저장할 res 변수를 0으로 초기화해준다.
3.  추출하려고 하는 수를 저장한 arr 를 순회하면서 break 명령이 떨어질 때 까지 while 반복한다.
4.  만약 큐의 첫번째 원소가 뽑아내려는 수와 일치 하는 경우, 바로 원소를 뽑아낸 뒤 while을 종료한다
5.  만약 큐의 첫번째 원소가 뽑아내려는 수와 일치 하지 않는 경우,
    1.  큐의 길이를 2로 나눈 몫이 큐에서 뽑아 내려는 값의 인덱스보다 크거나 같다면 왼쪽에서 원소를 뽑아 오른쪽에 붙인다.
    2.  큐의 길이를 2로 나눈 몫이 큐에서 뽑아 내려는 값의 인덱스보다 작다면 오른쪽에서 원소를 뽑아 왼쪽에 붙인다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from collections import deque

n, m = map(int, stdin.readline().split())
arr = list(map(int, stdin.readline().split()))
q = deque()
for i in range(1, n + 1):
    q.append(i)
res = 0

for i in arr:
    while 1:
        if q[0] != i:
            if len(q) // 2 >= q.index(i):
                temp = q.popleft()
                q.append(temp)
                res += 1
            else:
                q.appendleft(q.pop())
                res += 1
        else:
            q.popleft()
            break

print(res)
```

<br>

### 💾 느낀점

1.  python 의 deque 는 매우 강력하다.
2.  appendleft는 두고두고 쓸 함수일 것 같다는 생각이 들었습니다.