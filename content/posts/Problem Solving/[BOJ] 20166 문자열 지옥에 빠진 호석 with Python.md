---
author: ["Jxun-h"]
title: "[BOJ] 20166 문자열 지옥에 빠진 호석 with Python"
date: "2022-06-04"
description: ""
summary: ""
tags: ["자료구조", "PS", "DFS", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/20166" target="_blank">BOJ 20166 문자열 지옥에 빠진 호석</a>

<br>

### 💡 조건

1.  정신을 차려보니 바닥에는 격자 모양의 타일이 가득한 세상이었고, 각 타일마다 알파벳 소문자가 하나씩 써있다더라.  
    두려움에 가득해 미친듯이 앞만 보고 달려 끝을 찾아 헤맸지만 이 세상은 끝이 없었고,  
    달리다 지쳐 바닥에 드러누우니 하늘에 이런 문구가 핏빛 구름으로 떠다니고 있었다.

2.  이 세상은 N행 M열의 격자로 생겼으며, 각 칸에 알파벳이 써있고 환형으로 이어진다. 왼쪽 위를 (1, 1), 오른쪽 아래를 (N, M)이라고 하자.  
    너는 아무 곳에서나 시작해서 상하좌우나 대각선 방향의 칸으로 한 칸씩 이동할 수 있다. 이 때, 이미 지나 왔던 칸들을 다시 방문하는 것은 허용한다.  
    시작하는 격자의 알파벳을 시작으로, 이동할 때마다 각 칸에 써진 알파벳을 이어 붙여서 문자열을 만들 수 있다.  
    이 곳의 신인 내가 좋아하는 문자열을 K 개 알려줄 터이니, 각 문자열 마다 너가 만들 수 있는 경우의 수를 잘 대답해야 너의 세계로 돌아갈 것이다.  
    경우의 수를 셀 때, 방문 순서가 다르면 다른 경우이다. 즉, (1,1)->(1,2) 로 가는 것과 (1,2)->(1,1) 을 가는 것은 서로 다른 경우이다.

3.  너가 1행에서 위로 가면 N 행으로 가게 되며 반대도 가능하다.  
    너가 1열에서 왼쪽으로 가면 M 열로 가게 되며 반대도 가능하다.  
    대각선 방향에 대해서도 동일한 규칙이 적용된다.  
    하늘에 아래와 같은 그림을 구름으로 그려줄 터이니 이해해 돕도록 하여라.  
    예를 들어서, 너가 (1, 1)에서 위로 가면 (N, 1)이고, 왼쪽으로 가면 (1, M)이며 왼쪽 위 대각선 방향으로 가면 (N, M)인 것이다.

<br>
<center><img src='/20166.png'></center>
<br>

4.  세상을 이루는 격자의 정보와, K 개의 문자열이 주어졌을 때, 호석이가 대답해야 하는 정답을 구하는 문제.  
    **16개 이상의 데이터를 맞아야 AC를 받는다.**

5.  첫번째 줄에 격자의 크기 N, M과 신이 좋아하는 문자열의 개수 K 가 주어진다.  
    다음에 N개의 줄에 걸쳐서 M개의 알파벳 소문자가 공백없이 주어진다. 여기서의 첫 번째 줄은 1행의 정보이며, N 번째 줄은 N행의 정보이다.  
    이어서 K개의 줄에 걸쳐서 신이 좋아하는 문자열이 주어진다. 모두 알파벳 소문자로 이루어져 있다.

6.  3 ≤ N, M ≤ 10, N과 M은 자연수이다.  
    1 ≤ K ≤ 1,000, K는 자연수이다.  
    1 ≤ 신이 좋아하는 문자열의 길이 ≤ 5  
    신이 좋아하는 문자열은 중복될 수도 있다.

6.  **DFS, 깊이 우선 탐색** 유형의 문제

<br>

## 🔖 예제 및 실행결과

#### 예제

```py
3 4 3
abcb
bcaa
abac
aba
abc
cab
```

#### 실행결과

```py
56
0
```

<br>

## ⌨️ 문제 풀이

1.  n개의 입력을 받아 arr 리스트에 저장한다.

2.  k번 반복하면서 신이 좋아하는 문자열 을 입력 받아 ans에 키 값으로 두고, 0으로 초기화 한다.  
    또한 ans_list 에 신이 좋아하는 문자열을 저장한다.

3.  n * m 크기의 리스트를 순회하면서 각 좌표에 해당하는 문자로부터 시작해 만약 문자가 ans 에 있다면 + 1을 해준다.

4.  8방향으로 뻗어나가면서 재귀를 통해 solve() 힘수를 다시 타면서 cnt 파라미터가 5 이상이면 return 한다.

5.  n * m 크기의 리스트를 모두 순회했다면, ans_list 를 순회한다.(k)

6.  k 가 ans 에 있다면, ans 딕셔너리에 k 에 해당하는 키 값의 value를 출력하면 된다.

<br>

### 🖥 소스 코드

```py
from sys import stdin, setrecursionlimit

setrecursionlimit(10 ** 9)

n, m, k = map(int, stdin.readline().split())
ans, arr, res = {}, [], []
dx, dy = [1, 0, -1, 0, 1, 1, -1, -1], [0, 1, 0, -1, -1, 1, 1, -1]
ans_list = []

for i in range(n):
    arr.append(list(stdin.readline().rstrip()))

for _ in range(k):
    data = stdin.readline().rstrip()
    ans[data] = 0
    ans_list.append(data)


def solve(x, y, cnt, string):
    if cnt > 5:
        return

    if string in ans:
        ans[string] += 1

    for i in range(8):
        nx, ny = (x + n + dx[i]) % n, (y + m + dy[i]) % m
        solve(nx, ny, cnt + 1, string + arr[nx][ny])


for i in range(n):
    for j in range(m):
        start = ''
        solve(i, j, 1, start + arr[i][j])

for k in ans_list:
    if k in ans:
        print(ans[k])
```
