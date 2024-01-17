---
author: ["Jxun-h"]
title: "[BOJ] 16507 어두운 건 무서워 with Python"
date: "2021-09-12"
description: ""
summary: ""
tags: ["누적합", "PS", "prefix sum", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/16507" target="_blank">BOJ 16507 어두운 건 무서워</a>

<br>

## 💡 조건 및 풀이

1.  사진 크기를 의미하는 `1 <= R, C <= 1000`
2.  사진 일부분의 밝기 평균을 알아볼 개수 `Q`
3.  `Q`개의 각 줄에는 사진의 일부분을 나타내기 위한 두 꼭짓점을 의미하는 정수 `r1, c1, r2, c2` 가 주어진다.  
    `(1 ≤ r1 ≤ r2 ≤ R, 1 ≤ c1 ≤ c2 ≤ C)`
4.  **누적합 문제**
5.  `Q`개의 각 줄에 주어진 사진에서 두 점 `(r1, c1)`과 `(r2, c2)`를 **꼭짓점으로 하는 직사각형의 밝기 평균을 출력**한다.
6.  **평균은 정수 나눗셈으로 몫만 취한다.**

<br>

## 🔖 예제 및 실행결과

#### 예제

```python
5 6 1
4 1 3 4 9 5
1 2 8 7 5 5
8 1 2 5 3 2
1 5 3 4 2 5
5 2 1 2 3 5
2 2 4 5
```

#### 실행결과

```python
3
```

<br>

## ⌨️ 문제 풀이

1.  **누적합 문제다.**
2.  꼭지점을 의미하는 정수가 1부터 시작되기에 인덱스 에러를 조심해야한다.  
    그래서 나는 `(R + 1) * (C + 1)` 크기릐 배열을 만들어 코드도 단순화 시켰다.
3.  입력 받은 `R * C` 크기의 데이터를 배열에 넣고 누적합을 구해 배열에 넣어준다.
4.  꼭지점 좌표를 입력받아 `x`좌표의 크기를 오픔차순으로 정렬시켰다.  
    가장 왼쪽에 위치하고 있는 좌표를 찾으려고 했다.
5.  직사각형의 크기를 알아야 누적합을 이용해 찾은 밝기의 합도 나눌 수 있다.  
    그래서 정렬 시킨 좌표를 사용해 직사각형의 크기를 계산했다.
    
    ```python
    (abs(addr[0][0]-addr[1][0]) + 1) * (abs(addr[0][1]-addr[1][1]) + 1)
    ```
    
6.  배열의 각 가로줄마다 따로 계산을 해주었다.  
    누적합의 성질은 예를 들자면 다음과 같다.  
    **`[4, 5, 8, 12, 21, 26]` 의 배열이 있을 때, 배열의 두번째 원소부터 네번째 원소의 합을 구하려고한다.  
    그렇다면 네번째 원소에서 첫번째 원소의 값을 빼주면 구하려는 값이 된다.**

<br>

## 🖥 소스 코드

```python
from sys import stdin

r, c, q = map(int, stdin.readline().split())
pic = [[0] * (c + 1)]
for i in range(r):
    sum_list = [0]
    data = list(map(int, stdin.readline().split()))
    sum_list.append(data[0])
    for i in range(1, c):
        sum_list.append(sum_list[-1] + data[i])
    pic.append(sum_list)

for _ in range(q):
    a, b, c, d = map(int, stdin.readline().split())
    addr = [(a, b), (c, d)]
    addr.sort(key=lambda x: x[0])
    res = 0

    knife = (abs(addr[0][0]-addr[1][0]) + 1) * (abs(addr[0][1]-addr[1][1]) + 1)
    for i in range(addr[0][0], addr[1][0] + 1):
        res += pic[i][addr[1][1]] - pic[i][addr[0][1] - 1]

    print(res // knife)
```

<br>

## 💾 느낀점

-   누적합의 개념과 원리, 성질을 아르바이트 출근하면서 지하철에서 본 것이 큰 도움이 되었다.
-   인덱스 에러가 쉽게 발생할 수 있을 것 같다는 생각이 들어 다른 풀이도 생각해보았지만 큰 도움은 되지 않았다.