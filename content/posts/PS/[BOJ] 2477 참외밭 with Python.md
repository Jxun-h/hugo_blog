---
author: ["Jxun-h"]
title: "[BOJ] 2477 참외밭 with Python"
date: "2022-02-14"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2477" target="_blank">BOJ 2477 참외밭</a>

<br>

### 💡 조건

1.  m2의 넓이에 자라는 참외의 개수를 나타내는 양의 정수 K (1 ≤ K ≤ 20)
2.  참외밭을 나타내는 육각형의 임의의 한 꼭짓점에서 출발하여  
    반시계방향으로 둘레를 돌면서 지나는 변의 방향과 길이 (1 이상 500 이하의 정수)
3.  변의 방향에서 동쪽은 1, 서쪽은 2, 남쪽은 3, 북쪽은 4로 나타낸다.
4.  참외밭은 ㄱ-자 모양이거나 ㄱ-자를 90도, 180도, 270도 회전한 모양(┏, ┗, ┛ 모양)의 육각형이다.
5.  **구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
7
4 50
2 160
3 30
1 60
3 20
1 100
```

#### 실행결과

```py
47600
```

<br>

### ⌨️ 문제 풀이

1.  6개의 방향과 변의 길이를 각각 direction, length 라는 변수에 입력받는다  
    동시에, 변의 길이는 nums 리스트에 저장해주고, direction이 1 이거나 2 일 때 x 리스트에, 아닐 경우에는 y 리스트에 저장한다.
2.  x 축으로 움직이는 변의 길이 중 가장 긴 것을 max_x 에 저장한다.  
    y 축으로 움직이는 변의 길이 중 가장 긴 것을 max_y 에 저장한다.
3.  (2)에서 구한 max_x, max_y 값이 x 리스트, y 리스트에서 인덱스 값이 몇인지 구한다.
4.  가장 긴 가로변(xi) 양측에 있는 가로 변의 길이 의 차이가 전체 사각형 길이에서 내가 빼줄 사각형의 가로 길이  
    만약 xi + i 가 6보다 크거나 같으면 nums[xi-1] - nums[0]
5.  가장 긴 세로변(xi) 양측에 있는 세로 변의 길이 의 차이가 전체 사각형 길이에서 내가 빼줄 사각형의 세로 길이  
    만약 yi + i 가 6보다 크거나 같으면 nums[yi-1] - nums[0]
6.  사각형 최대 넓이 - 작은 사각형의 넓이를 구한다.
    -   사각형 최대 넓이 : max_x * max_y
    -   작은 사각형 넓이 : x * y
7.  면적 당 참외의 개수를 출력해야하니, (6)에서 구한 면적에 * n 을 해준 값을 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
nums = []
x, y = [], []
for _ in range(6):
    direction, length = map(int, stdin.readline().split())
    nums.append(length)
    if direction == 1 or direction == 2:
        x.append(length)
    else:
        y.append(length)

max_x = max(x)
max_y = max(y)
xi = nums.index(max_x)
yi = nums.index(max_y)

if xi + 1 >= 6:
    x = abs(nums[xi - 1] - nums[0])
else:
    x = abs(nums[xi - 1] - nums[xi + 1])

if yi + 1 >= 6:
    y = abs(nums[yi - 1] - nums[0])
else:
    y = abs(nums[yi - 1] - nums[yi + 1])

print(((max_x * max_y) - (x * y)) * n)
```

<br>

### 💾 느낀점

1.  문제 풀이에 써놓은 4, 5번 을 떠올리지 못해서 헤맸던 문제였다.
2.  블로그를 쓰려고 다시 보는데 또 헷갈려서 다시 풀었다.
3.  이런 수학적인 사고를 하는 문제, DP 문제는 아직도 어렵다.
4.  연습만이 살길이다. 다시 한 번 쓰면서 생각해보고 풀어서 다행이라고 생각한다.