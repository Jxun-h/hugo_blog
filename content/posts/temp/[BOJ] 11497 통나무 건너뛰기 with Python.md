---
author: ["Jxun-h"]
title: "[BOJ] 11497 통나무 건너뛰기 with Python"
date: "2021-12-06"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/11497" target="_blank">BOJ 11497 통나무 건너뛰기</a>

<br>

### 💡 조건

1.  첫 줄에 통나무의 개수를 나타내는 정수 `(5 ≤ N ≤ 10,000)`  
    둘째 줄에 각 통나무의 높이를 나타내는 정수 `(1 ≤ Li ≤ 100,000)`
2.  통나무 건너뛰기의 난이도는 인접한 두 통나무 간의 높이의 차의 최댓값으로 결정된다.  
    **가장 첫 통나무와 가장 마지막 통나무 역시 인접해 있다.**
3.  **그리디 알고리즘**유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
3
7
13 10 12 11 10 11 12
5
2 4 5 7 9
8
6 6 6 6 6 6 6 6
```

#### 실행결과

```python
1
4
0
```

<br>

### ⌨️ 문제 풀이

1.  단순히 정렬을 해도 되지만, 첫 통나무와 마지막 통나무가 인접해있다는 조건이 있다.
2.  1번에서 말한 조건 때문에, 가장 큰 값을 기준으로 양쪽에 점점 작게 배치를 하면  
    크기의 차이를 가장 많이 줄일 수 있다.
3.  즉, 인덱스 값이 2씩 차이나는 값들 중 가장 큰 값이 최대 높이 차가 된다.

<br>

### 🖥 소스 코드

```python
from sys import stdin

for _ in range(int(stdin.readline())):
    n = int(stdin.readline())
    arr = list(map(int, stdin.readline().split()))
    arr.sort()
    res = 0
    for i in range(2, n):
        res = max(res, abs(arr[i] - arr[i-2]))
    print(res)
```

### 💾 느낀점

1.  문제 풀이에서 2번과 3번에 대해서 이해하지 못해서 힘이 들었다.
2.  이해하고 다시 풀어보기를 반복해야할 문제이다.
3.  2021/12/06 다시 풀어보았는데 또 틀렸다. 해설을 보니 기억이 나긴하는데 또 이해가 안된다.