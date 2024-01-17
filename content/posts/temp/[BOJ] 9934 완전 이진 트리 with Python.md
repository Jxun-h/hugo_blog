---
author: ["Jxun-h"]
title: "[BOJ] 9934 완전 이진 트리 with Python"
date: "2021-09-12"
description: ""
summary: ""
tags: ["트리", "PS", "완전이진트리", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/9934" target="_blank">BOJ 9934 완전 이진 트리</a>

<br>

## 💡 조건 및 풀이

1.  이진 트리의 깊이를 나타내는 `1<=K<=10`, 깊이가 `K`인 이진 트리는 총 `2 * K - 1` 개의 노드로 이루어져 있다.
2.  **가장 마지막 레벨을 제외한 모든 집은 왼쪽 자식과 오른쪽 자식을 갖는다.**
3.  **이분탐색, 트리, 재귀구현 문제**
4.  모든 빌딩의 번호는 중복되지 않는다.

<br>

## 🔖 예제 및 실행결과

#### 예제

```python
3
1 6 4 3 5 2 7
```

#### 실행결과

```python
3
6 2
1 4 5 7
```

<br>

## ⌨️ 문제 풀이

1.  깊이가 `k` 인 2차원 리스트 `res` 를 생성하고, 이 리스트에 노드를 쌓을 것입니다.
2.  Python 리스트 자료구조의 `extend()` 함수를 사용했습니다.  
    `extend`는 리스트를 리스트 안으로 넣을 때 리스트의 원소만 넣어줍니다.
3.  입력받은 빌딩번호의 길이를 2로 나누어 값을 `mid` 변수에 넣어 가지고 있습니다.
4.  `res`에 파라미터로 받은 `depth` 값을 넣어줍니다.  
    가장 맨 처음으로 이분탐색을 통해 뽑아낸 가운데 값이 루트 노드입니다.
5.  가운데 값을 기준으로 양쪽을 분리해 각각 다시 이분탐색을 수행합니다.
6.  이분 탐색을 하다가, 파라미터로 받은 `arr` 리스트의 길이가 1인 경우 `depth` 에 해당하는  
    리스트에 넣어줍니다.
7.  만들어진 트리(`res`)를 출력해줍니다.
8.  파이썬으로 재귀를 구현할 때,아래의 함수를 사용해야 에러가 나지 않는 경우가 많습니다.  
    쓴다고 문제될 것이 없으니, 재귀를 구현하여 문제를 푸실 때 꼭 입력하세요.  
     
9.  `setrecursionlimit(int(1e9))​`

<br>

## 🖥 소스 코드

```python
from sys import stdin, setrecursionlimit
setrecursionlimit(int(1e9))
k = int(stdin.readline())
arr = list(map(int, stdin.readline().split()))
res = [[] for _ in range(k)]


def binary_separation(arr, depth):
    if len(arr) == 1:
        res[depth].extend(arr)
        return

    length = len(arr)
    mid = length // 2
    res[depth].append(arr[mid])
    binary_separation(arr[:mid], depth + 1)
    binary_separation(arr[mid + 1:], depth + 1)


binary_separation(arr, 0)

for i in range(k):
    if i == 0:
        print(res[i][0])
    else:
        print(*res[i])
```

<br>

## 💾 느낀점

-   이분탐색과 재귀를 사용하여 문제를 푸는 방식에 익숙해진 것을 느꼈다.
-   분할 정복 문제를 풀다가 이 문제를 푸니 훨씬 도움이 되었다.