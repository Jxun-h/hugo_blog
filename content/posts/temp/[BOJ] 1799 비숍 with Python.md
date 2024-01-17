---
author: ["Jxun-h"]
title: "[BOJ] 1799 비숍 with Python"
date: "2021-10-11"
description: ""
summary: ""
tags: ["백트래킹", "PS", "재귀", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1799" target="_blank">BOJ 1799 비숍</a>

<br>

## 💡 조건 및 풀이

1.  **체스판의 크기는 10 이하의 자연수**
2.  비숍을 놓을 수 있는 곳에는 `1`, 비숍을 놓을 수 없는 곳에는 `0`
3.  대각선 방향으로 움직이는 비숍이 이동할 수 있는 경로에 비숍을 놓을 수 없다.
4.  **백트래킹 유형의 문제**

<br>

## 🔖 예제 및 실행결과

#### 예제

```
5
1 1 0 1 1
0 1 0 0 0
1 0 1 0 1
1 0 0 0 0
1 0 1 1 1
```

#### 실행결과

```
7
```

<br>

## ⌨️ 문제 풀이

1.  흑과 백을 구분할 수 있는 체스판을 `True` 와 `False` 를 사용해 다시 만든다.
2.  비숍을 놓을 수 있는 좌표를 흑과 백으로 나누어 각각 `black` 과 `white` 리스트에 넣어준다.
3.  비숍을 놓고, 놓을 수 없는 곳을 표시할 때 사용할 `isused` 리스트를 생성한다.
4.  재귀함수를 타고 각 좌표에 해당하는 곳이 `isused01`, `isused02` 모두 사용 중이거나  
    놓을 수 없는 자리라면 `index`를 하나 늘리고 다시 재귀.
5.  `4번`에 해장하지 않으면 비숍을 놓고 놓은 비숍 개수와 `index`를 1씩 늘리고 재귀
6.  재귀를 빠져나오면 **직전에 놓았던 비숍의 정보를 제거하고 다음 좌표로 넘어가기 위해 `index + 1` 하고 재귀**
7.  `index`값이 흰색 혹은 검정색 비숍 좌표의 길이와 같다면 검정색의 최댓값과 흰색의 최댓값을 각각 `Bcnt`와 `Wcnt`에 저장한다.

<br>

## 🖥 소스 코드

```python
from sys import stdin

n = int(stdin.readline())

chess_map = []
black = []
white = []
color = [[0] * n for _ in range(n)]

for i in range(n):
    for j in range(n):
        color[i][j] = (i % 2 == 0 and j % 2 == 0) or (i % 2 != 0 and j % 2 != 0)

for i in range(n):
    chess_map.append(list(map(int, input().split())))
    for j in range(n):
        # True가 검은색
        if chess_map[i][j] == 1 and color[i][j] == 1:
            black.append((i, j))
        # False가 흰색
        if chess_map[i][j] == 1 and color[i][j] == 0:
            white.append((i, j))

# 검은색인 경우
Bcnt = 0
# 흰색인 경우
Wcnt = 0

isused01 = [0] * (n * 2 - 1)
isused02 = [0] * (n * 2 - 1)


def fun(bishop, index, count):
    global Bcnt, Wcnt
    if index == len(bishop):
        rx, ry = bishop[index - 1]
        # 블랙이면 Bcnt 최대값
        if color[rx][ry]:
            Bcnt = max(Bcnt, count)
        # 흰색이면 Wcnt 최대값
        else:
            Wcnt = max(Wcnt, count)
        return

    x, y = bishop[index]
    if isused01[x + y] or isused02[x - y + n - 1]:
        fun(bishop, index + 1, count)
    else:
        isused01[x + y] = 1
        isused02[x - y + n - 1] = 1
        fun(bishop, index + 1, count + 1)
        isused01[x + y] = 0
        isused02[x - y + n - 1] = 0
        fun(bishop, index + 1, count)


if len(black) > 0:
    fun(black, 0, 0)
if len(white) > 0:
    fun(white, 0, 0)
print(Bcnt + Wcnt)
```

<br>

## 💾 느낀점

-   무지성 백트래킹으로 풀려다가 시간초과가 떴다.
-   백트래킹을 잘하려면 재귀를 잘 짤줄 알아야하는데 아직도 재귀함수가 약점이다.
-   흑, 백 칸을 구분지어 구현하는데에도 헷갈리는 부분이 있었다.
-   함수를 구현하고서도 이해가 안되는 부분이 있어서 별표를 많이 쳐놨다.
-   다시는 풀고 싶지 않은 유형이지만, 그래도 옛날보다는 나아지는 느낌을 받는다.  
    다시 풀어봐야겠다.