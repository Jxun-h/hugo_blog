---
author: ["Jxun-h"]
title: "[BOJ] 15658 연산자 끼워넣기 (2) with Python"
date: "2022-02-02"
description: ""
summary: ""
tags: ["자료구조", "PS", "백트래킹", "DFS", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/15658" target="_blank">BOJ 15658 연산자 끼워넣기 (2)</a>

<br>

### 💡 조건

1.  N개의 수로 이루어진 수열 A1, A2, ..., AN  
    N(2 ≤ N ≤ 11), (1 ≤ Ai ≤ 100)
2.  입력 값중 셋째 줄에 4N보다 작거나 같은 4개의 정수가 주어지는데,  
    차례대로 덧셈(+)의 개수, 뺄셈(-)의 개수, 곱셈(×)의 개수, 나눗셈(÷)의 개수이다.
3.  수와 수 사이에 연산자를 하나씩 넣어서, 수식을 하나 만들 수 있다. 이때, **주어진 수의 순서를 바꾸면 안 된다.**
4.  식의 계산은 연산자 우선 순위를 무시하고 앞에서부터 진행해야 한다.
5.  나눗셈은 정수 나눗셈으로 몫만 취한다. 또한 음수를 나눌 때에는 양수로 바꾼 뒤 몫을 취하고, 그 몫을 음수로 바꾸어야 한다.
6.  **백트래킹, DFS 알고리즘 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
6
1 2 3 4 5 6
3 2 1 1
```

#### 실행결과

```py
72
-48
```

<br>

### ⌨️ 문제 풀이

1.  DFS 알고리즘과 백트래킹을 이용한 문제 풀이를 했다.
2.  DFS에 매개변수로 들어가는 val 의 값은 수열의 순서를 바꾸면 안되기 때문에 무슨 짓을 해도 수열\[0\] 의 값과 같다.
3.  DFS에 매개변수로 들어가는 num은 입력받은 수열의 index 1번부터 들어가면 된다.
4.  DFS가 종료되는 시점은 **num 이라는 리스트가 비어있을 때**이며 이 때, 최댓값과 최솟값을 갱신하면서 종료된다.  
    최댓값은 -int(1e9), 최솟값은 int(1e9)이다.
5.  arr 리스트는 각각 덧셈(+), 뺄셈(-), 곱셈(×), 나눗셈(÷)의 개수이며, 입력으로 받는다.
6.  만약 DFS가 넘겨받는 num 리스트가 비어있지 않다면, 반복문을 0부터 3까지 반복을 한다.  
    반복하면서, 각 i 의 숫자에 따라 arr\[i\]의 값이 0보다 클 때, val 변수에 해당하는 연산을 해준 뒤, 재귀호출을 한다.
7.  재귀호출을 할 때, num\[1:\] 을 매개변수로 넘겨주어 중복 계산을 방지한다.  
    이렇게 재귀호출을 하게 되면 넘겨주는 리스트는 길이가 앞에서부터 하나씩 없어지게 되는데,  
    재귀 호출 전, arr\[i\]를 -1 해주고 재귀 호출 후 +1 해준다.

<br>

### 🖥 소스 코드

```py
from sys import stdin, setrecursionlimit
setrecursionlimit(10 ** 6)

n = int(stdin.readline())
n_num = list(map(int, stdin.readline().split()))
arr = list(map(int, stdin.readline().split()))


def dfs(num, val):
    global max_res, min_res
    if not num:
        max_res = max(val, max_res)
        min_res = min(val, min_res)
        return
    else:
        for i in range(4):
            if i == 0:
                if arr[i] > 0:
                    arr[i] -= 1
                    dfs(num[1:], val + num[0])
                    arr[i] += 1
                else:
                    continue

            if i == 1:
                if arr[i] > 0:
                    arr[i] -= 1
                    dfs(num[1:], val - num[0])
                    arr[i] += 1
                else:
                    continue

            if i == 2:
                if arr[i] > 0:
                    arr[i] -= 1
                    dfs(num[1:], val * num[0])
                    arr[i] += 1
                else:
                    continue

            if i == 3:
                if arr[i] > 0:
                    arr[i] -= 1
                    if val < 0:
                        temp = abs(val) // num[0] * -1
                    else:
                        temp = val // num[0]
                    dfs(num[1:], temp)
                    arr[i] += 1
                else:
                    continue


max_res = -int(1e9)
min_res = int(1e9)
dfs(n_num[1:], n_num[0])
print(max_res, min_res, sep='\n')
```

<br>

## 💾 느낀점

1.  단순히 permutations 혹은 combinations 로 풀지 않았고,  
    정확하게 DFS 및 백트래킹을 활용하여 풀이했는데, 이것이 N과 M 시리즈를 푸는데에 좋은 연습이 됐다.
2.  조건이 크게 없었지만, division error를 조심해야 했고,  
    음수일 경우에 나눗셈의 방식이 조금 다르기 때문에 간단한 조건 추가하는 것만 조심하면 되는 문제였던 것 같다.