---
author: ["Jxun-h"]
title: "[BOJ] 6010 Music Notes with Python"
date: "2022-06-03"
description: ""
summary: ""
tags: ["자료구조", "PS", "이분탐색", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/6010" target="_blank">BOJ 6010 Music Notes</a>

<br>

### 💡 조건

1.  노래는 음표 N개로 구성되며, i 번째 음표는 B_i 비트동안 지속된다.  
    N(1 <= N <= 50,000), B_i(1 <= B_i <= 10,000)  
    어떤 노래도 5억 비트 보다 길지 않다.

2.  0에서 노래를 연주하기 시작하며, 0에서부터 B_1 전까지 음표 1개, 시간 B_1에서 B_1 + B_2 직전까지 음표 2개를 연주한다.

3.  T 시간부터 T+1 직전까지의 간격에서 어떤 음표를 연주해야하는지 구하는 문제.

4.  질문의 개수는 Q개가 있다.  
    Q(1 <= Q <= 50,000)

5.  질문은 T_i(0 <= T_i <= end_of_song)으로 제공된다.

6.  **이분탐색 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3 5
2
1
3
2
3
4
0
1
```

#### 실행결과

```py
2
3
3
1
1
```

<br>

### ⌨️ 문제 풀이

1.  노트를 저장할 때, 해당 노트의 범위 X가 (a <= X < b)에 해당한다면, 최댓값 (b-1)만 저장한다.

2.  T_i 부분에서 이분탐색을 사용한다.  
    이분 탐색을 사용하여 나온 end 값에서 +1 을 해주고 출력하면 된다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = map(int, stdin.readline().split())
nums = []
now = 0


def solve(start, end, target):
    while end > start:
        mid = (start + end) // 2
        if nums[mid] < target:
            start = mid + 1
        else:
            end = mid
    return end


for _ in range(n):
    count = int(stdin.readline())
    nums.append(now + count - 1)
    now += count
nums.append(int(1e12))

for _ in range(m):
    j = int(stdin.readline())
    it = solve(0, len(nums), j)
    print(it + 1)
```

<br>

### 💾 느낀점

1.  이분탐색을 통해서 해야겠다는 생각을 못한 것 같다.

2.  영어로 된 문제의 지문을 해석해 문제를 풀이하는데 있어서 어려움을 겪었다.