---
author: ["Jxun-h"]
title: "[BOJ] 2615 오목 with Python"
date: "2021-12-12"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2615" target="_blank">BOJ 2615 오목</a>

<br>

### 💡 조건

1.  바둑판에는 19개의 가로줄과 19개의 세로줄이 그려져 있다. **board의 크기는 `19 * 19`**

2.  `검은 바둑알은 1`, `흰 바둑알은 2`, `알이 놓이지 않는 자리는 0`으로 표시

3.  가로, 세로 또는 대각선 방향 모두 포함해서 같은 색의 바둑돌이 5개 놓여져 있다면 승리한다.  
    **5개 초과 또는 미만의 개수는 승리할 수 없다**

4.  검은색이 이겼는지, 흰색이 이겼는지 또는 아직 승부가 결정되지 않았는지를 판단하는 프로그램을 작성.  
    검은색이 이겼을 경우에는 1을, 흰색이 이겼을 경우에는 2를, 아직 승부가 결정되지 않았을 경우에는 0을 출력

5.  은색 또는 흰색이 이겼을 경우에는 둘째 줄에 연속된 다섯 개의 바둑알 중에서 가장 왼쪽에 있는 바둑알의 가로줄, 세로줄 번호를 출력한다.
    -   세로로 놓인 경우, 그 중 가장 위에 있는 바둑알의 가로, 세로줄 번호를 출력한다.

6.  **브루트포스 알고리즘 & 구현 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 1 2 0 0 2 2 2 1 0 0 0 0 0 0 0 0 0 0
0 0 1 2 0 0 0 0 1 0 0 0 0 0 0 0 0 0 0
0 0 0 1 2 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 1 2 2 0 0 0 0 0 0 0 0 0 0 0 0
0 0 1 1 0 1 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 2 1 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0
```

#### 실행결과

```python
1
3 2
```

<br>

### ⌨️ 문제 풀이

1.  바둑판은 `19 * 19`의 크기로 제한되어 있다. `solve()` 함수에서 이중 반복문으로 바둑판의 칸을 모두 순회한다.

2.  순회하면서 검은 바둑돌이 놓여진 곳과 흰 바둑알이 놓여진 곳을 발견하게 된다면, `check()` 함수를 호출한다.
    -   check(돌의 색, x 좌표, y 좌표)  
        의 형식으로 호출하여 반환 받은 결과가 빈 배열이 아니라면, 이긴 바둑 돌의 색의 번호와 바둑돌의 좌표들을 반환한다.

3.  `check()` 함수는 오른쪽, 아래, 좌측 아래, 우측 아래의 네 방향을 검사한다.  
    입력받은 좌표를 기준으로 위에서 말한 네 방향을 검사하면서, **넘겨받은 바둑돌의 색깔과 일치하는 돌**이 있다면  
    res 집합 자료형 변수에 넣어주고, `5`개인지 확인하여 맞다면 `res`를 `list`로 변환하여 `반환`, 아니라면 `반복문을 종료`한다.

4.  `solve()` 함수 호출 후 작업이 끝났다면, `code` 와 `v`를 반환받게 되는데,  
    `code`는 이긴 바둑돌을 뜻하며 `v`는 바둑돌의 좌표들을 뜻한다.

5.  세로로 세워진 바둑돌인지 확인 한 후, `tf`의 값에 따라 `v`를 정렬하고 이긴 바둑돌의 색과 좌표를 출력한다.  
    `tf` 가 1일 때, 세로로 놓여진 다섯개의 바둑돌이다.  
    `tf` 가 0일 때, 세로가 아닌 방향으로 놓여진 바둑돌이다.
6.  `solve()` 함수에 반환받은 `v`가 `False` 라면 무승부이기 때문에 `0`을 출력한다.

<br>

### 🖥 소스 코드

```python
from sys import stdin

dx, dy = [0, 1, 1, 1], [1, 0, -1, 1]

board = []
visited = [set() for _ in range(4)]

for i in range(19):
    board.append(list(map(int, stdin.readline().split())))


def check(code, i, j):
    for z in range(4):
        cnt = 1
        res = set()
        res.add((i, j))

        nx, ny = i + dx[z], j + dy[z]

        while 1:
            if 0 <= nx < 19 and 0 <= ny < 19:
                if board[nx][ny] == code and ((nx, ny) not in visited[z]):
                    cnt += 1
                    res.add((nx, ny))
                    visited[z].add((nx, ny))
                    nx += dx[z]
                    ny += dy[z]
                else:
                    if cnt == 5:
                        return list(res)
                    else:
                        break
            else:
                if cnt == 5:
                    return list(res)
                break
    return []


def solve():
    for i in range(19):
        for j in range(19):
            if board[i][j] == 1:
                v = check(1, i, j)
                if v:
                    return 1, v
            elif board[i][j] == 2:
                v = check(2, i, j)
                if v:
                    return 2, v
    return 0, False


code, v = solve()
if v is False:
    print(0)
else:
    tf = 1
    x = v[0][1]
    for i in range(1, 5):
        if x != v[i][1]:
            tf = 0
            break

    if tf:
        v.sort(key=lambda x: (x[0]))
        print(code)
        print(*(v[0][0] + 1, v[0][1] + 1))
    else:
        print(code)
        v.sort(key=lambda x: (x[1]))
        print(*(v[0][0] + 1, v[0][1] + 1))
```

<br>

### 💾 느낀점

1.  바둑돌이 여섯개 일 때 조건문을 통해 걸러내는 법에서 헤맸다.
2.  구현을 할 때 조금 더 꼼꼼히 생각해보자.