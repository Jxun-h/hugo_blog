---
author: ["Jxun-h"]
title: "[BOJ] 2342 Dance Dance Revolution with Python"
date: "2022-05-20"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2342" target="_blank">BOJ 2342 Dance Dance Revolution</a>

<br>

### 💡 조건

1.  편의상 중점을 0, 위를 1, 왼쪽을 2, 아래를 3, 오른쪽을 4라고 정하자.

<br>
    <center><img src='/2342.png' width="381" height="381" /></center>
<br>

2.  처음에 게이머는 두 발을 중앙에 모으고 있다.(그림에서 0의 위치)  
    그리고 게임이 시작하면, 지시에 따라 왼쪽 또는 오른쪽 발을 움직인다. 하지만 그의 두 발이 동시에 움직이지는 않는다.

3.  두 발이 같은 지점에 있는 것이 허락되지 않는다.  
    한 발이 1의 위치에 있고, 다른 한 발이 3의 위치에 있을 때, 3을 연속으로 눌러야 한다면, 3의 위치에 있는 발로 반복해야 눌러야 한다.

4.  발을 이동할 때 힘을 사용하게 된다.
    1.  중앙에 있던 발이 다른 지점으로 움직일 때, 2의 힘을 사용하게 된다.
    2.  다른 지점에서 인접한 지점으로 움직일 때는 3의 힘을 사용하게 된다.
    3.  반대편으로 움직일때는 4의 힘을 사용하게 된다.
    4.  같은 지점을 한번 더 누른다면, 그때는 1의 힘을 사용하게 된다.

5.  입력은 지시 사항으로 이루어진다. 각각의 지시 사항은 하나의 수열로 이루어진다.  
    각각의 수열은 1, 2, 3, 4의 숫자들로 이루어지고, 이 숫자들은 각각의 방향을 나타낸다.  
    입력 파일의 마지막에는 0이 입력된다. 입력되는 수열의 길이는 100,000을 넘지 않는다.

6.  **다이나믹프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
1 2 2 4 0
```

#### 실행결과

```py
8
```

<br>

### ⌨️ 문제 풀이

1.  문제를 간단하게 말하자면, 최소한의 힘을 사용해 입력받은 수열의 번호를 다 눌러야한다.

2.  다시 말해, 왼쪽 발과 오른쪽 발이 어느 위치에 있을 때, 어떤 발판부터 밟아야 최소의 힘을 들일 수 있는가? 이다.

3.  그렇다면 이 문제는 solve(n, l, r) 이라고 간단하게 함수처럼 만들어 볼 수가 있다.  
    발의 위치가 (l,r) 일 때 n번째 팔판부터 밟았을 때 소모되는 힘이라고 정의할 수 있다.

4.  발은 동시에 움직일 수 없으니, 발이 움직이는 건 2가지가 있다.  
    solve(n, l, r) 은 왼쪽 발을 움직여 발판을 밟은 상태와 오른쪽 발을 움직여 발판을 밟은 상태의 최솟값이 될 수 있다.
5.  그렇다면 아래와 같이 정의할 수 있다.

    ```py
    min(solve(n + 1, arr[n], r) + move(l, arr[n]), solve(n + 1, l, arr[n]) + move(r, arr[n]))
    ```

<br>

## 🖥 소스 코드

```py
import sys

sys.setrecursionlimit(10 ** 6)


def move(a, b):
    if a == b:
        return 1
    elif a == 0:
        return 2
    elif abs(b - a) % 2 == 0:
        return 4
    else:
        return 3


def solve(n, l, r):
    global dp
    if n >= len(arr) - 1:
        return 0

    if dp[n][l][r] != -1:
        return dp[n][l][r]

    dp[n][l][r] = min(solve(n + 1, arr[n], r) + move(l, arr[n]), solve(n + 1, l, arr[n]) + move(r, arr[n]))
    return dp[n][l][r]


arr = list(map(int, sys.stdin.readline().split()))
dp = [[[-1] * 5 for _ in range(5)] for _ in range(100000)]

print(solve(0, 0, 0))
```

<br>

### 💾 느낀점

1.  메모이제이션과 재귀함수를 통해 결과값을 도출하는 방법