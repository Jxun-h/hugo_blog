---
author: ["Jxun-h"]
title: "[BOJ] 1094 막대기 with Python"
date: "2022-02-01"
description: ""
summary: ""
tags: ["자료구조", "PS", "DFS", "수학", "비트마스킹", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1094" target="_blank">BOJ 1094 막대기</a>

<br>

### 💡 조건

1.  64cm인 막대를 가지고 있다.  
    지민이는 원래 가지고 있던 막대를 더 작은 막대로 자른다음에, 풀로 붙여서 길이가 Xcm인 막대를 만들려고 한다.
2.  아래는 막대를 자르는 방법이다.  
    1) 지민이가 가지고 있는 막대의 길이를 모두 더한다.  
    처음에는 64cm 막대 하나만 가지고 있다. 이때, 합이 X보다 크다면, 아래와 같은 과정을 반복한다.  
    1-1) 가지고 있는 막대 중 길이가 가장 짧은 것을 절반으로 자른다.  
    1-2) 만약, 위에서 자른 막대의 절반 중 하나를 버리고 남아있는 막대의 길이의 합이 X보다 크거나 같다면,2) 이제, 남아있는 모든 막대를 풀로 붙여서 Xcm를 만든다.
3.  `위에서 자른 막대의 절반 중 하나를 버린다.`
4.  X는 64보다 작거나 같은 자연수
5.  **DFS, 수학, 비트마스킹 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
23
```

#### 실행결과

```py
4
```

<br>

### ⌨️ 문제 풀이

1.  DFS 알고리즘을 사용해서 풀이했다.
2.  결과값을 저장할 res 변수와 분리되지 않은 막대기 64가 들어가있는 sticks 리스트를 생성한다.
3.  solve() 함수의 로직은 아래와 같습니다.
    -   sticks 리스트의 합이 입력받은 값 x 보다 클 경우,  
        sticks 에서 heapq.heappop() 함수를 통해 가장 작은 값을 빼낸다.  
        빼낸 값을 2로 나눈 몫을 다시 heapq.heappush()로 다시 넣어준다.
    -   만약, sticks 리스트의 합에서 heapq.heappop() 함수를 통해 가장 작은 값을 뺀 값이 x보다 크거나 같다면  
        heapq.heappop() 함수를 통해 가장 작은 값을 빼낸다.  
        solve() 함수를 재귀호출한다.
    -   위의 조건에 해당하지 않고, sticks의 리스트의 합이 x보다 크거나 같다면 다시 solve() 함수를 재귀호출한다.
4.  sticks 리스트의 길이를 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin, setrecursionlimit
import heapq
setrecursionlimit(10 ** 6)

x = int(stdin.readline())
res = 0
sticks = [64]


def solve(sticks):
    global res
    val = sum(sticks)

    if val > x:
        temp = heapq.heappop(sticks)
        heapq.heappush(sticks, temp // 2)
        heapq.heappush(sticks, temp // 2)

        if sum(sticks) - (temp // 2) >= x:
            heapq.heappop(sticks)
            solve(sticks)
        elif sum(sticks) >= x:
            solve(sticks)


solve(sticks)
print(len(sticks))
```

<br>

### 💾 느낀점

1.  heapq를 사용하여 재귀호출을 통해 답을 구하는 문제였습니다.
2.  막대기를 자르는 방법을 충실히 구현하여 재귀호출하는 방법을 사용한다면 어렵지 않게 풀 수 있는 문제였습니다.