---
author: ["Jxun-h"]
title: "[BOJ] 3151 합이 0 with Python"
date: "2022-06-01"
description: ""
summary: ""
tags: ["자료구조", "PS", "이분탐색", "투포인터", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/3151" target="_blank">BOJ 3151 합이 0</a>

<br>

### 💡 조건

1.  1 ≤ N ≤ 10000  
    -10000 ≤ Ai ≤ 10000

2.  대회는 정확히 3명으로 구성된 팀만 참가가 가능하다.

3.  코딩 실력이 좋으면 팀워크가 떨어지고, 팀워크가 좋을수록 코딩 실력이 떨어진다. 그리고 출전하고자 하는 대회는 코딩 실력과 팀워크 모두가 중요하다.  
    세 팀원의 코딩 실력의 합이 0이 되는 팀을 만들고자 한다.

4.  대회에 출전할 수 있는 팀을 얼마나 많이 만들 수 있는지를 계산하여라.

5.  N명의 학생들의 코딩 실력 Ai가 -10000부터 10000사이의 정수로 주어질 때, 합이 0이 되는 3인조를 만들 수 있는 경우의 수를 구하는 문제.

6.  **이분 탐색, 투 포인터** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
10
2 -5 2 3 -4 7 -4 0 1 -6
```

#### 실행결과

```py
6
```

#### 힌트

예시에서 가능한 참가자 그룹은 아래와 같다.

```py
(2, -5, 3), (2, 2, -4), (2, 2, -4), (-5, 2, 3), (3, -4, 1), (3, -4, 1)
```

두 개의 -4는 서로 다른 참가자를 나타내는 것에 유의하라. (2, 2, -4)와 (3, -4, 1)이 두 번씩 나타난다.

<br>

### ⌨️ 문제 풀이

1.  이분 탐색은 순서를 보장해야하는 리스트에서는 사용하지 못한다는 것을 인지하고 있어야 한다.  
    이분 탐색할 리스트를 정렬해준다.  
    3151번 문제는 순서와 상관없이 3명의 인원을 뽑아 코딩 실력의 합이 0이 되는 조합을 찾아야 한다.

2.  입력을 받은 리스트의 길이의 -2 만큼 순회한다.  
    순회하는 숫자를 X 라고 할 때, X에서 두 숫자를 빼 0이 되는 경우를 투포인터 + 이분탐색을 통해 찾는다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
# 이분탐색

n = int(stdin.readline())
arr = list(map(int, stdin.readline().split()))
arr.sort()
ans = 0


def solve(s, e, g):
    global ans
    max_idx = n
    while s < e:
        tmp = arr[s] + arr[e]
        if tmp < goal:
            s += 1

        elif tmp == g:
            if arr[s] == arr[e]:
                ans += e - s

            else:
                if max_idx > e:
                    max_idx = e
                    while max_idx >= 0 and arr[max_idx - 1] == arr[e]:
                        max_idx -= 1
                ans += e - max_idx + 1
            s += 1
        else:
            e -= 1


for i in range(n - 2):
    start = i + 1
    end = n - 1
    goal = -arr[i]
    solve(start, end, goal)

print(ans)
```