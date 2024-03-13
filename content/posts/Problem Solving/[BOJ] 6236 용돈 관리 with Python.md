---
author: ["Jxun-h"]
title: "[BOJ] 6236 용돈 관리 with Python"
date: "2022-06-17"
description: ""
summary: ""
tags: ["자료구조", "PS", "이분탐색", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/6236" target="_blank">BOJ 6236 용돈 관리</a>

<br>

### 💡 조건

1.  현우는 앞으로 N일 동안 자신이 사용할 금액을 계산하였고, 돈을 펑펑 쓰지 않기 위해 정확히 M번만 통장에서 돈을 빼서 쓰기로 하였다.

2.  현우는 통장에서 K원을 인출하며, 통장에서 뺀 돈으로 하루를 보낼 수 있으면 그대로 사용하고,  
    모자라게 되면 남은 금액은 통장에 집어넣고 다시 K원을 인출한다.

3.  다만 현우는 M이라는 숫자를 좋아하기 때문에, 정확히 M번을 맞추기 위해서 남은 금액이 그날 사용할 금액보다  
    많더라도 남은 금액은 통장에 집어넣고 다시 K원을 인출할 수 있다.

4.  현우는 돈을 아끼기 위해 인출 금액 K를 최소화하기로 하였다. 현우가 필요한 최소 금액 K를 계산하는 문제.

5.  1번째 줄에는 N과 M이 공백으로 주어진다. (1 ≤ N ≤ 100,000, 1 ≤ M ≤ N)  
    2번째 줄부터 총 N개의 줄에는 현우가 i번째 날에 이용할 금액이 주어진다. (1 ≤ 금액 ≤ 10000)  
    첫 번째 줄에 현우가 통장에서 인출해야 할 최소 금액 K를 출력한다.

6.  **이분탐색** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
7 5
100
400
300
100
500
101
400
```

#### 실행결과

```py
500
```

<br>

### ⌨️ 문제 풀이

1.  i번째 날에 이용할 금액을 리스트에 저장해주고 가장 작은 값을 start, 가장 큰 값을 end로 설정해준다.

2.  구할 인출금액을 mid = (start + end) // 2로 정해주고, 인출한 횟수 cnt를 1로 설정한다.

3.  리스트를 순회하면서(x : 현재 순회하는 리스트의 인덱스에 해당하는 금액) 최소 인출금액 - x 의 값이 0보다 작으면  
    인출금액 money를 mid 로 저장한다.  
    만약 이 조건에 해당하지 않는다면 money - i 값으로 money를 갱신한다.

4.  arr 리스트를 모두 순회한 후, 출금 횟수가 m 을 넘어선 경우 혹은 mid 값이 arr의 값보다 작은 경우는  
    start 를 mid + 1 값으로 갱신한다.

5.  (4)번의 조건에 해당하지 않는다면, end 값을 end - 1 로 갱신한다.  
    또한 ans의 값을 mid 로 갱신한다.

6.  이분탐색이 끝나면 ans 의 값을 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n, m = map(int, stdin.readline().split())
arr = []
for _ in range(n):
    arr.append(int(stdin.readline()))

start = min(arr)
end = sum(arr)

while start <= end:
    mid = (start + end) // 2
    money = mid
    cnt = 1

    for i in arr:
        if money - i < 0:
            money = mid
            cnt += 1
        money -= i

    if cnt > m or mid < max(arr):
        start = mid + 1
    else:
        end = mid - 1
        ans = mid

print(ans)
```
