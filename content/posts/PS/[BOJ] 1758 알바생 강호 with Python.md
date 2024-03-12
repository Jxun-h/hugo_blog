---
author: ["Jxun-h"]
title: "[BOJ] 1758 알바생 강호 with Python"
date: "2022-03-17"
description: ""
summary: ""
tags: ["자료구조", "PS", "정렬", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1758" target="_blank">BOJ 1758 알바생 강호</a>

<br>

### 💡 조건

1.  손님들은 입구에 들어갈 때, 강호에게 팁을 준다. 손님들은 자기가 커피를 몇 번째 받는지에 따라 팁을 다른 액수로 강호에게 준다.
2.  각 손님은 강호에게 원래 주려고 생각했던 돈 - (받은 등수 - 1) 만큼의 팁을 강호에게 준다.
3.  만약, 위의 식으로 나온 값이 음수라면, 강호는 팁을 받을 수 없다.
4.  사람의 수 N과, 각 사람이 주려고 생각하는 팁이 주어질 때, 손님의 순서를 적절히 바꿔 강호가 받을 수 잇는 팁의 최댓값을 구하는 문제
5.  N은 100,000보다 작거나 같은 자연수이다. 팁은 100,000보다 작거나 같은 자연수이다.
6.  **정렬** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4
3
3
3
3
```

#### 실행결과

```py
6
```

<br>

### ⌨️ 문제 풀이

1.  각 손님이 지불할 돈이 담긴 리스트를 입력받아 내림차순으로 정렬한다.
2.  가장 돈을 많이 낼 손님이 첫번째 등수가 되어야 최댓값을 구할 수 있다.
3.  계산식을 사용해 각 손님에게 받을 수 있는 팁의 금액을 더해 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

res, n = 0, int(stdin.readline())
arr = []
for i in range(n):
    arr.append(int(stdin.readline()))

arr.sort(reverse=True)

for i in range(1, n + 1):
    tips = arr[i-1] - (i - 1)
    if tips > 0:
        res += tips

print(res)
```

<br>

### 💾 느낀점