---
author: ["Jxun-h"]
title: "[BOJ] 14469 소가 길을 건너간 이유 3 with Python"
date: "2023-04-01 22:41:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "정렬", "그리디", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/14469" target="_blank">BOJ 14469 소가 길을 건너간 이유 3</a>

<br>

### 💡 조건

1.  N마리의 소가 이 농장에 방문하러 왔다. 소가 도착한 시간과 검문받는 데 걸리는 시간은 소마다 다르다. (물론 같을 수도 있다.)

2.  두 소가 동시에 검문을 받을 수는 없다. 예를 들어, 한 소가 5초에 도착했고 7초 동안 검문을 받으면,  
    8초에 도착한 그 다음 소는 12초까지 줄을 서야 검문을 받을 수 있다.

3.  모든 소가 농장에 입장하려면 얼마나 걸리는지 구하는 문제.

4.  첫 줄에 100 이하의 양의 정수 N이 주어진다.
5.  다음 N줄에는 한 줄에 하나씩 소의 도착 시각과 검문 시간이 주어진다. 각각 1,000,000 이하의 양의 정수이다.

5.  **정렬, 그리디** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
3
2 1
8 3
5 7
```

#### 실행결과 1

```py
15
```

<br>

### ⌨️ 문제 풀이

1.  기본 아이디어는 정렬부터 시작을 했다. 모든 소가 입장하려면 얼마나 걸리는지, 최소시간을 출력하는 문제이다.

2.  소가 모두 입장하는데에 걸리는 최소 시간을 찾으려면, 입장하는 번호를 기준으로 정렬을 해야한다.

3.  소가 도착한 시간과 검문 받는데 걸리는 시간은 같을 수 있으므로, lambda 로 정렬 시켰다.  
    기준은 (소가 도착한 시간, 검문 받는 시간) 을 각각 오름차순으로 정렬했다.

4.  정렬된 리스트를 순회하면서, 만약 현재 흐른 시간(ans)가 소가 도착한 시간(s) 보다 작거나 같다면 ans에 s를 넣어준다.  
    그 후 ans에 검문시간을 더해준다.
5.  (4)번에 예외되는 조건이라면 그냥 ans에 c를 더해주고 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
arr = []

for _ in range(n):
    a, b = map(int, stdin.readline().split())
    arr.append((a, b))

arr.sort(key=lambda x: (x[0], x[1]))

ans = 0

for i in range(n):
    s, c = arr[i][0], arr[i][1]
    if ans <= s:
        ans = s
        ans += c

    else:
        ans += c

print(ans)
```