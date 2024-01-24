---
author: ["Jxun-h"]
title: "[BOJ] 2343 기타 레슨 with Python"
date: "2021-10-19"
description: ""
summary: ""
tags: ["이분탐색", "PS", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2343" target="_blank">BOJ 2343 기타 레슨</a>

<br>

### 💡 조건

1.  강의의 수 N `(1 ≤ N ≤ 100,000)`  
    블루레이의 수 M `(1 ≤ M ≤ N)`
2.  **블루레이를 녹화할 때, 강의의 순서가 바뀌면 안 된다.**
3.  각 강의의 길이가 분 단위(자연수)로 주어진다. **가능한 블루레이의 크기 중 최소를 구하는 문제.**
4.  **이분탐색 알고리즘 유형의 문제**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
9 3
1 2 3 4 5 6 7 8 9
```

#### 실행결과

```python
17
```

<br>

### ⌨️ 문제 풀이

1.  이분탐색을 위해 `left`, `right`, `mid` 변수를 초기화 해줍니다.
    -   left는 입력받은 강의 시간 배열의 가장 큰 값
    -   right는 입력받은 강의 시간 배열의 합
    -   mid = (left + right) // 2

2.  블루레이의 크기에 몇개의 강의가 들어가는지 검사하여 반환하는 함수를 만들어줍니다.  
    여기서 블루레이의 크기는 mid를 기준으로 검사를 해준다.
3.  `def get_cnt(): count = 0 temp = 0 for i in range(n): if temp + arr[i] > mid: count += 1 temp = 0 temp += arr[i] if temp: count += 1 return count`

3.  `left`변수가 `right` 변수보다 크거나 같을 때까지 반복하여 진행한 뒤, `left`, `right`, `mid` 중 가장 큰 값을 출력한다.  
    블루레이의 크기가 모두 같아야하기 때문에 최댓값을 출력하는 것이다.

<br>

### 🖥 소스 코드

```python
from sys import stdin

n, m = map(int, stdin.readline().split())
arr = list(map(int, stdin.readline().split()))


def get_cnt():
    count = 0
    temp = 0
    for i in range(n):
        if temp + arr[i] > mid:
            count += 1
            temp = 0
        temp += arr[i]

    if temp:
        count += 1

    return count


left, right = max(arr), sum(arr)
while left <= right:
    mid = (left + right) // 2
    cnt = get_cnt()
    if cnt > m:
        left = mid + 1
    elif cnt <= m:
        right = mid - 1

print(max(left, right, mid))
```

<br>

### 💾 느낀점

1.  이분탐색을 통해서 풀어내는 문제였다.
2.  문제를 이해하지 못해서 조금 헤맸던 문제였다.
3.  `get_cnt` 함수를 구현하려다가 순서가 바뀌면 안된다는 조건을 보고 구현할 수 있었다.