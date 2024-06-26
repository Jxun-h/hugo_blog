---
author: ["Jxun-h"]
title: "[BOJ] 2302 극장 좌석 with Python"
date: "2022-03-31"
description: ""
summary: ""
tags: ["자료구조", "PS", "DP", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2302" target="_blank">BOJ 2302 극장 좌석</a>

<br>

### 💡 조건

1.  어떤 극장의 좌석은 한 줄로 되어 있으며 왼쪽부터 차례대로 1번부터 N번까지 번호가 매겨져 있다.  
    공연을 보러 온 사람들은 자기의 입장권에 표시되어 있는 좌석에 앉아야 한다.
2.  자기의 바로 왼쪽 좌석 또는 바로 오른쪽 좌석으로는 자리를 옮길 수 있다.
3.  이 극장에는 “VIP 회원”들이 있다. 이 사람들은 반드시 자기 좌석에만 앉아야 하며 옆 좌석으로 자리를 옮길 수 없다.
4.  오늘 공연은 입장권이 매진되어 1번 좌석부터 N번 좌석까지 모든 좌석이 다 팔렸다.  
    VIP 회원들의 좌석 번호들이 주어졌을 때, 사람들이 좌석에 앉는 서로 다른 방법의 가짓수를 구하는 프로그램을 작성하시오.
5.  N은 1 이상 40 이하이다. 둘째 줄에는 고정석의 개수 M이 입력된다.  
    방법의 가짓수는 2,000,000,000을 넘지 않는다. (2,000,000,000 < 231-1)
6.  **다이나믹프로그래밍** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
9
2
4
7
```

#### 실행결과

```py
12
```

<br>

### ⌨️ 문제 풀이

1.  m 의 크기만 큼 수를 입력받아 vip 리스트에 저장한다.
2.  n의 값에 따라 가짓수를 정리하면 아래와 같다.  
    n = 0 일 때는 한가지로 본다.  
    n = 1 일 때는 1  
    n = 2 일 때는 2  
    n = 3 일 때는 3  
    n = 4 일 때는 5
3.  (2)번을 정리하면 피보나치 수열과 같다.  
    점화식은 dp[i] = dp[i-2] + dp[i-1] 이 되겠다.
4.  arr 리스트를 생성하고 피보나치 수열을 만들어준다.
5.  vip 가 있는 경우, vip는 제자리에만 있어야하기 때문에  
    vip의 수만큼 순회하면서 각 vip 자리 이전 번호에서 이전 vip 번호를 뺀 arr의 값까지의  
    경우의 수를 곱해준다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = int(stdin.readline()), int(stdin.readline())
vip = []

for _ in range(m):
    vip.append(int(stdin.readline()))

arr = [1, 1, 2]
for i in range(3, 41):
    arr.append(arr[i-2] + arr[i-1])


ans = 1

if m > 0:
    pre = 0
    for i in range(m):
        ans *= arr[vip[i] - 1 - pre]
        pre = vip[i]
    ans *= arr[n - pre]
else:
    ans = arr[n]
print(ans)
```

<br>

### 💾 느낀점

1.  다이나믹프로그래밍이 너무 어렵다는 것을 다시 한 번 느꼈다.
2.  점화식을 구현하지 못하는 부분에서 문제를 이해하지 못하는 것인가를 생각하고 처음부터 찬찬히 살펴본 문제였다.
3.  이해를 한 후, 블로그 포스팅을 하면서 다시 복기를 하니 처음보다 이해가 쉬웠다.
4.  (3)번처럼 쉬운 느낌을 받았다고 하나, 비슷한 유형을 풀 수 있을까? 라는 질문에는 자신있게 대답하지는 못하겠다.