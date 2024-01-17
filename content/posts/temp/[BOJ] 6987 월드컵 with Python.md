---
author: ["Jxun-h"]
title: "[BOJ] 6987 월드컵 with Python"
date: "2021-09-22"
description: ""
summary: ""
tags: ["백트래킹", "PS", "재귀", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/6987" target="_blank">BOJ 6987 월드컵</a>

<br>

## 💡 조건 및 풀이

1.  `6개의 국가`가 있고, `총 18번의 경기`를 한다.
2.  `승, 무, 패`의 결과가 있으며, `승, 무, 패`의 수는 `6보다 작거나 같은 자연수 또는 0`
3.  **백트래킹 유형의 문제**
4.  입력은 네 줄로 들어오며, 각 줄에 대해 `가능한 결과 1`, `불가능한 결과 0` 을출력하는 문제이다

<br>

## 🔖 예제 및 실행결과

#### 예제

```python
5 0 0 3 0 2 2 0 3 0 0 5 4 0 1 1 0 4
4 1 0 3 0 2 4 1 0 1 1 3 0 0 5 1 1 3
5 0 0 4 0 1 2 2 1 2 0 3 1 0 4 0 0 5
5 0 0 3 1 1 2 1 2 2 0 3 0 0 5 1 0 4
```

#### 실행결과

```python
1 1 0 0
```

<br>

## ⌨️ 문제 풀이

1.  `data` 변수에 각 나라의 일정을 담고, `res` 베열에 3개씩 쪼개어 다시 넣는다.
2.  결과를 담을 `ans` 변수를 0으로 초기화 시킨다.
3.  팀끼리의 경기의 조합을 위해 `itertools`의 `combinations`를 사용.  
    `game`이라는 변수에 **0~5번의 국가가 경기를 할 수 있는 조합을 만들어 저장**한다.
4.  `solution` 함수에서 총 라운드를 파라미터로 입력받으며, 초기의 값은 0이다.
5.  **각 라운드를 순회하면서 `res` 배열의 값을 빼주면서 승, 무, 패 의 값이 남아있다면**  
    `ans = 0`으로 초기화해서 불가능한 경기라고 `answer` 리스트에 저장하면 된다.
6.  승에 해당하는 원소를 -1 할 때, 패에 해당하는 원소를 -1 해준다.  
    무에 해당하는 원소를 -1 할 때, 무에 해당하는 다른 원소를 -1 해준다.
7.  `round` 값이 15라운드가 되었다면 `ans`의 값을 1로 변경하고 검사를 시작한다.  
    **`res` 변수에 있는 0의 값이 3개가 아니라면 `ans` 를 0으로 변경**

<br>

## 🖥 소스 코드

```python
from sys import stdin
from itertools import combinations as cb


def solution(round):
    global ans
    if round == 15:
        ans = 1
        for sub in res:
            if sub.count(0) != 3:
                ans = 0
                break
        return

    t1, t2 = game[round]
    for x, y in ((0, 2), (1, 1), (2, 0)):
        if res[t1][x] > 0 and res[t2][y] > 0:
            res[t1][x] -= 1
            res[t2][y] -= 1
            solution(round + 1)
            res[t1][x] += 1
            res[t2][y] += 1


answer = []
game = list(cb(range(6), 2))
# 백트래킹
for _ in range(4):
    data = list(map(int, stdin.readline().split()))
    res = [data[i:i + 3] for i in range(0, 16, 3)]
    ans = 0
    solution(0)
    answer.append(ans)

print(*answer)
```

<br>

## 💾 느낀점

-   백트래킹을 위해 재귀함수를 구현하여 조건을 풀어내는 일련의 과정이 힘겹다.  
    조금 더 백트래킹 및 재귀에 관한 문제를 풀어보아야겠다.
-   문제를 조금 더 내가 스스로도 납득하고 이해할 수 있게 풀어내는 방법을 생각해봐야겠다.
-   문제 및 로직에 대해 생각하는 시간이 너무 짧고, 문제를 풀기 위해 손부터 나가는 나쁜 습관을 고쳐야겠다.
-   아이디어를 떠올리지 못해 고생을 많이 했던 문제인 것 같다.  
    블로그에 글을 포스팅하면서 다시 한 번 정리하니 도움이 되는 것 같다.