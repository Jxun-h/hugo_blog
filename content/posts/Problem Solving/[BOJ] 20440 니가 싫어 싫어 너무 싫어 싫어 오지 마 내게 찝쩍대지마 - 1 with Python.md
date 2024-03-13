---
author: ["Jxun-h"]
title: "[BOJ] 20440 🎵니가 싫어 싫어 너무 싫어 싫어 오지 마 내게 찝쩍대지마🎵 - 1 with Python"
date: "2022-05-17"
description: ""
summary: ""
tags: ["자료구조", "PS", "imos", "누적합", "좌표압축", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/20440" target="_blank">BOJ 20440 니가 싫어 싫어 너무 싫어 싫어 오지 마 내게 찝쩍대지마 - 1</a>

<br>

### 💡 조건

1.  어떤 모기가 방에 언제 입장했고 언제 퇴장했는지를 기록할 수 있다.
2.  방에 출입한 모기의 마릿수 N(1 ≤ N ≤ 1,000,000)
3.  N개의 줄에 모기의 입장 시각 TE과 퇴장 시각 TX이 주어진다. (0 ≤ TE < TX ≤ 2,100,000,000)  
    모기는 [TE, Tx)동안 존재한다.
4.  첫째 줄에 지동이 방에 모기가 가장 많이 있는 시간대의 모기 마릿수를 출력한다.  
    방에 모기가 가장 많이 있는 시간대의 연속 구간 전체를 [TEm, TXm)이라고 할 때,  
    둘째 줄에 TEm, TXm을 공백으로 구분하여 출력한다.  
    **단, 여러 가지 방법이 있으면 가장 빠른 시작 시각을 기준으로 출력한다.**
5.  모기들의 방 입장, 퇴장 시각이 주어졌을 때 모기들이 가장 많이 있는 시간대와 해당 시간대에 모기가 몇 마리가 있는지 구하는 문제
6.  **imos, 누적 합, 좌표압축** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제 1

```py
3
2 16
4 6
6 10
```

#### 실행결과 1

```py
2
4 10
```

![예제 1](https://upload.acmicpc.net/e6a3a59c-b626-48eb-ac61-92582a7d9332/-/preview/)

#### 예제 2

```py
3
0 16
0 6
0 10
```

#### 실행결과 2

```py
3
0 6
```

<br>

### ⌨️ 문제 풀이

1.  먼저, 나는 좌표 압축 + imos 알고리즘을 통해 문제를 풀이했다.

2.  좌표압축이란 **모든 구간이 아니라, 중요한 구간 혹은 숫자만 들고있는 기법**이다.  
    순위가 중요한 알고리즘에서 입력값의 개수 < 입력값의 범위일때 사용한다.

3.  문제에서 주어지는 모기들이 존재하는 시간은 최대 100만 개이다.  
    모기들이 존재할 수 있는 시간대는 0에서 최대 21억까지이기 때문에 모든 구간을 순회하면서 구간합을 구할 수는 없다.  
    따라서 (2)번에서 설명한 좌표압축을 통해 내가 필요한, 중요한 구간의 번호만 관리해야 한다.

4.  이 때, 모기들이 존재할 수 있는 구간은 최대 200만개의 정보가 되기에 중요한 정보를 모두 리스트에 넣어 관리할 수 있다.

5.  (4)번의 생각을 구현하기 위해서 나는 time_set = set() 집합 자료형을 통해 중복을 제거했다.  
    이 set() 자료형의 길이 + 1만큼 리스트를 생성했다.  
    생성한 리스트에 각 모기의 좌표를 update 해주면 중복제거가 되며, 이를 다시 리스트로 만들어주고 정렬한다.

6.  (5)번의 작업을 진행하면서, 각 시간대를 저장할 time 리스트에 각 구간을 tuple로 묶어넣어 관리한다.  
    예제 1번을 예로 들었을 때, set() 자료형에는 {2, 4, 6, 10, 16} 이 들어가 있고, 이를 기준으로 만든 배열을 대응 시키면  
    2는 인덱스 0, 4는 인덱스 1에 대응된다.

7.  대응되는 관계를 dictionary 자료형을 사용해 저장해주면 관리가 쉽다.

8.  time_set 의 길이 + 1만큼 생성한 리스트는 imos 알고리즘을 사용해 구간을 갱신시킬 것.

9.  imos 알고리즘이란, 각 쿼리가 구간 [s, e] 내의 값을 갱신시키는 경우,  
    이를 **매 쿼리마다 일일히 갱신하지 않고**, **시작과 끝만 기록**해두었다가 마지막에 한 번의 처리로 값을 시뮬레이팅하는 방법이다.  
    **아무리 많은 쿼리가 있더라도, O(N)의 시간을 보장한다.**(개사기)

10.  모기가 존재하는 구간의 정보를 담아두었던 time을 순회하면서,
    1.  모기가 있는 구간의 시작(s) 시간이 prefix 리스트에 대응하는 원소값에 +1을 해준다.  
        이는 dictionary[s] += 1 을 통해서 쉽게 할 수 있다.
    2.  모기가 있는 구간의 끝(e) 시간이 prefix 리스트에 대응하는 원소값에 -1을 해준다.

11.  이제 prefix 리스트를 순회하면서 구간합을 구해주며, 이 prefix 리스트의 max값을 구해 max_val에 저장한다.

12.  문제 지문에서 **단, 여러 가지 방법이 있으면 가장 빠른 시작 시각을 기준으로 출력한다.** 라고 했다.  
    prefix를 순회하면서 max_val이 어느 인덱스부터 시작하는지 저장하고, 어느 구간에서 달라지는지 저장한 뒤, 출력하면 된다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
time = []
time_set = set()

for i in range(n):
    s, e = map(int, stdin.readline().split())
    time.append((s, e))
    time_set.update([s, e])

d = {}
cnt = 0
time_set = list(time_set)
time_set.sort()
for i in time_set:
    d[i] = cnt
    cnt += 1

prefix = [0 for _ in range(len(time_set) + 1)]

for s, e in time:
    prefix[d[s]] += 1
    prefix[d[e]] -= 1

max_val = 0

for i in range(len(time_set)):
    prefix[i] = prefix[i] + prefix[i - 1]
    if prefix[i] > max_val:
        max_val = prefix[i]

print(max_val)
ans = [0, 0]
tf = False
for i in range(len(time_set) + 1):
    if prefix[i] == max_val and not tf:
        ans[0] = time_set[i]
        tf = True

    if prefix[i] != max_val and tf:
        ans[1] = time_set[i]
        break

print(*ans)
```

<br>

### 💾 느낀점

1.  imos 알고리즘, 구간합의 확장
2.  좌표압축을 통해 관리하려는 데이터의 수 최소화하기
3.  (1), (2) 를 통해 prefix 를 할 때, 큰 범위를 좁게 좁혀 구할 수 있는 방법