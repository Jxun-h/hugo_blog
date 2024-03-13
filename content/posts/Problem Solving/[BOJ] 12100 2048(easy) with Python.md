---
author: ["Jxun-h"]
title: "[BOJ] 12100 2048(easy) with Python"
date: "2021-10-25"
description: ""
summary: ""
tags: ["구현", "PS", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/12100" target="_blank">BOJ 12100 2048(easy)</a>

<br>

### 💡 조건

1.  보드의 크기는 `N * N` `(1 ≤ N ≤ 20)`  
    `0` 은 빈칸, 이외의 값은 블록의 값들을 나타낸다.  
    블록에 쓰여 있는 수는 `2보다 크거나 같고, 1024보다 작거나 같은 2의 제곱꼴`이다.  
    블록은 적어도 하나 주어진다.
2.  같은 값을 갖는 두 블록이 충돌하면 두 블록은 하나로 합쳐지게 된다.
3.  **한 번의 이동에서 이미 합쳐진 블록은 또 다른 블록과 다시 합쳐질 수 없다.**
4.  `최대 다섯번 이동` 시켜서 얻을 수 있는 가장 큰 블록의 값을 출력.
5.  **백트래킹 알고리즘 유형의 문제**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
3
2 2 2
4 4 4
8 8 8
```

#### 실행결과

```python
16
```

<br>

### ⌨️ 문제 풀이

1.  `백트래킹은 재귀가 가장 핵심.`  
    백트래킹을 수행하며 재귀를 진행할 `recursive`함수에 파라미터를 `cnt` 로 주고, 첫 실행시에는 `0`을 주고 실행시킨다.

2.  N의 크기가 작기 때문에 `deep copy`를 이용한 배열복사가 가능하다.  
    이를 통해 방향을 바꾸기 전, **이전 보드의 상태를 기억하기 위한 소스코드를 작성한다.**  
    움직이기 전 보드의 상황을 기억해두지 않으면, 백트래킹이 수행될 수 없다.
    
    ```python
    b = [x[:] for x in arr]
    ```
    

3.  네 방향으로 블록을 움직일 수 있으니, 반복문을 통해 네 방향으로 움직여준다.  
    `move()` 함수에서 `k` 의 값에 따라 네 방향으로 움직여 준다.
    
    ```python
    def move(k):
     # arr[i][j]
     if k == 0:  # 위로 이동, 블락들이 위로 모두 이동하면 row index는 0
         for j in range(n):
             for i in range(n):
                 get(i, j)
             merge(0, j, 1, 0)  # row index 1씩 증가하면서 아래쪽 블락들을 합쳐감
     elif k == 1:  # 아래로 이동, 블락들이 아래로 모두 이동하면 row index는 n-1
         for j in range(n):
             for i in range(n - 1, -1, -1):
                 get(i, j)
             merge(n - 1, j, -1, 0)  # row 인덱스 1씩 감소하면서 위쪽들을 합쳐감
     elif k == 2:  # 오른쪽으로 이동, column index는 0
         for i in range(n):
             for j in range(n):
                 get(i, j)
             merge(i, 0, 0, 1)  # column 인덱스 증가 오른쪽으로 이동
     else:  # 왼쪽으로 이동, column index는 n-1
         for i in range(n):
             for j in range(n - 1, -1, -1):
                 get(i, j)
             merge(i, n - 1, 0, -1)  # column 인덱스 감소 왼쪽으로 이동
    ```
    

4.  `get()` 함수에서 움직일 보드들의 상태를 확인하면서 순차적으로 순회해주고,  
    순회하면서 배열 원소의 값이 `0`이 아닌 경우, 원소의 값을 `큐`에 넣어준다.  
    배열에 넣은 값이 있던 해당 자리는 `0`으로 바꿔준다.
    
    ```python
    def get(i, j):
     if arr[i][j]:  # 0이 아닌 값이라면
         q.append(arr[i][j])  # queue에 arr의 값을 넣는다.
         arr[i][j] = 0  # 처리가 된 빈 자리는 0으로 값 업데이트
    ```
    

5.  `merge()` 함수에서 각 이동하려는 방향에 알맞게 인덱스를 조절하며 큐가 빌때까지 반복하며 합쳐준다.  
    움직이려는 값의 블록을 `큐`에서 꺼내온 후, 놓을 곳의 블럭의 값이 `0`이라면 그냥 두고,  
    값이 일치한다면 **2의 제곱 꼴이기에 2배**를 해준다.  
    값이 일치 하지 않는다면 그 자리에 그대로 둔다.

    ```python
    def merge(i, j, di, dj):  # row index, column index, y방향, x방향
        while q:
            x = q.popleft()  # 움직이려는 블록 값을 가져온다. FIFO
            if not arr[i][j]:  # 0이라면 그대로 놓는다.
                arr[i][j] = x
            elif arr[i][j] == x:  # 값이 일치한다면
                arr[i][j] = x * 2  # 합쳐지므로 2배로 증가
                i, j = i + di, j + dj
            else:  # 값이 일치하지 않으면
                i, j = i + di, j + dj
                arr[i][j] = x
    ```

6.  `move()` 함수의 처리가 끝났다면, `cnt + 1` 을 파라미터로 주고, `recursive` 함수를 재귀호출 해준다.

7.  `3번`부터 다시 반복하면서, `cnt 값이 5, 즉 다섯번 움직였을 때`, 보드판을 순회한다.  
    각 배열의 최댓값과 정답으로 출력할 `ans` 값을 비교하여 갱신한다.

<br>

### 🖥 소스 코드

```python
from sys import stdin, setrecursionlimit
from collections import deque

setrecursionlimit(int(1e9))

n = int(stdin.readline())
arr = [list(map(int, stdin.readline().split())) for _ in range(n)]
answer, q = 0, deque()


def get(i, j):
    if arr[i][j]:  
        q.append(arr[i][j])  
        arr[i][j] = 0  


def merge(i, j, di, dj):  
    while q:
        x = q.popleft()  
        if not arr[i][j]:  
            arr[i][j] = x
        elif arr[i][j] == x:  
            arr[i][j] = x * 2  
            i, j = i + di, j + dj
        else:  
            i, j = i + di, j + dj
            arr[i][j] = x


def move(k):

    if k == 0:  
        for j in range(n):
            for i in range(n):
                get(i, j)
            merge(0, j, 1, 0)  
    elif k == 1:  
        for j in range(n):
            for i in range(n - 1, -1, -1):
                get(i, j)
            merge(n - 1, j, -1, 0)  
    elif k == 2:  
        for i in range(n):
            for j in range(n):
                get(i, j)
            merge(i, 0, 0, 1)  
    else:  
        for i in range(n):
            for j in range(n - 1, -1, -1):
                get(i, j)
            merge(i, n - 1, 0, -1)  


def recursive(count):
    global arr, answer
    if count == 5:  
        for i in range(n):
            answer = max(answer, max(arr[i]))  
        return
    b = [x[:] for x in arr]  

    for k in range(4):  
        move(k)  
        recursive(count + 1)  
        arr = [x[:] for x in b]


recursive(0)
print(answer)
```

<br>

### 💾 느낀점

1.  재귀함수를 얼마나 응용을 할 수 있는지에 대한 문제였다.
2.  get(), move() 함수를 구현하는 것이 가장 어려웠으며, 이 부분은 다른 블로그에서 아이디어를 얻어 해결했다.
3.  몇 번이고 다시 풀어보기 좋은 문제인 것 같다. 주말에 다시 한 번 풀어보는 것이 좋겠다.