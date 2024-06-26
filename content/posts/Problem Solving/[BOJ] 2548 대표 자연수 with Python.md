---
author: ["Jxun-h"]
title: "[BOJ] 2548 대표 자연수 with Python"
date: "2022-07-12 15:52:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "이분탐색", "정렬", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2548" target="_blank">BOJ 2548 대표 자연수</a>

<br>

### 💡 조건

1.  정보초등학교의 연아는 여러 개의 자연수가 주어졌을 때, 이를 대표할 수 있는 대표 자연수에 대하여 연구하였다.  
    그 결과 어떤 자연수가 다음과 같은 성질을 가지면 대표 자연수로 적당할 것이라고 판단하였다.  
    “대표 자연수는 주어진 모든 자연수들에 대하여 그 차이를 계산하여 그 차이들 전체의 합을 최소로 하는 자연수이다.”

2.  예를 들어 주어진 자연수들이 [4, 3, 2, 2, 9, 10]이라 하자.  
    이때 대표 자연수는 3 혹은 4가 된다.  
    왜냐하면 (4와 3의 차이) + (3과 3의 차이) + (2와 3의 차이) + (2와 3의 차이) + (9와 3의 차이) + (10과 3의 차이) = 16,  
    (4와 4의 차이) + (3과 4의 차이) + (2와 4의 차이) + (2와 4의 차이) + (9와 4의 차이) + (10과 4의 차이) = 16으로 같다.

3.  첫째 줄에는 자연수의 개수 N이 입력된다. N은 1 이상 20,000 이하이다.  
    둘째 줄에는 N개의 자연수가 빈칸을 사이에 두고 입력되며, 이 수들은 모두 1 이상 10,000 이하이다.

4.  **이분탐색, 정렬** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
6
4 3 2 2 9 10
```

#### 실행결과

```py
3
```

<br>

### ⌨️ 문제 풀이

1.  이 문제는 이분탐색 문제이다. N이 최대 20000 이고, 각 숫자의 차이를 일일히 구하면 반드시 TLE 이다.

2.  최솟값을 0으로, 최댓값을 int(1e9)로 둔 뒤, 이분탐색을 통해서 mid 값을 정해준다

3.  정해준 mid 값으로 입력받은 리스트의 각 원소값과의 차이를 더해 최소가 되는지 계산한다.

4.  계산한 대표 자연수가 기존의 대표 자연수보다 작다면 갱신해준다.

<br>

### 🖥 소스 코드

```py
from sys import stdin


n = int(stdin.readline())
arr = list(map(int, stdin.readline().split()))
arr.sort()

l, r = 0, n
res = int(1e9)
ans = max(arr)

while l <= r:
    mid = (l + r) // 2
    temp = sum([abs(x - arr[mid]) for x in arr])

    if temp <= res:
        ans = min(ans, arr[mid])
        res = temp
        r = mid - 1

    else:
        l = mid + 1

print(ans)
```
