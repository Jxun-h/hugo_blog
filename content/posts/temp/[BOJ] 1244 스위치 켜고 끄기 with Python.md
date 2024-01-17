---
author: ["Jxun-h"]
title: "[BOJ] 1244 스위치 켜고 끄기 with Python"
date: "2021-10-17"
description: ""
summary: ""
tags: ["구현", "PS", "시뮬레이션", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1244" target="_blank">BOJ 1244 스위치 켜고 끄기</a>

<br>

## 💡 조건 및 풀이

1.  첫째 줄은 스위치 개수. `스위치 개수는 100 이하인 양의 정수.`  
    둘째 줄은 각 스위치의 상태. `켜져 있으면 1, 꺼져있으면 0이라고 표시`  
    셋째 줄에는 학생 수. `학생수는 100 이하인 양의 정수`  
    넷째 줄부터 마지막 줄까지 한 줄에 한 학생의 성별, 학생이 받은 수.
2.  남학생은 스위치 번호가 자기가 받은 수의 배수이면, 그 스위치의 상태를 바꾼다. 즉, 스위치가 켜져 있으면 끄고, 꺼져 있으면 켠다.
3.  여학생은 자기가 받은 수와 같은 번호가 붙은 스위치를 중심으로 좌우가 대칭이면서 가장 많은 스위치를 포함하는 구간을 찾아서,  
    그 구간에 속한 스위치의 상태를 모두 바꾼다. **이때 구간에 속한 스위치 개수는 항상 홀수가 된다.**
4.  **구현 & 시뮬레이션 유형의 문제**
5.  학생들은 입력되는 순서대로 자기의 성별과 받은 수에 따라 스위치의 상태를 바꾸었을 때, **스위치들의 마지막 상태를 출력하는 문제.**

<br>

## 🔖 예제 및 실행결과

#### 예제

```python
8
0 1 0 1 0 0 0 1
2
1 3
2 3
```

#### 실행결과

```python
1 0 0 0 1 1 0 1
```

<br>

## ⌨️ 문제 풀이

1.  학생의 수만큼 순회하여 남자일 때와 여자일 때를 구분하여 작업을 할 수 있도록 조건문을 짠다.  
    (내가 문제를 푸는 방식은 이러하다. 이렇게 큰 틀을 짜놓고 구현하면 훨씬 편하다.)
2.  남자는 지문에 나오는 것처럼, 스위치의 상태가 1일 때 0으로, 0일 때 1로 변경해주면 된다.
3.  여자의 경우, 좌우로 대칭하는지 찾기 전에, 현재 학생이 받은 수에 1씩 더하고 빼서 스위치로 입력받은 리스트 범위 내인지부터 확인한다.  
    범위 내인 경우, 현재 번호의 양쪽 데이터가 같은지 확인하고, 일치한다면 left, right 변수에 좌측, 우측의 인덱스 번호를 넣어준다.
4.  while 반복문으로 양측의 데이터가 같지 않을 때, 리스트의 범위를 벗어날 때 break를 걸어주고  
    left와 right를 갱신한다.
5.  while 반복이 끝난 후, range(left, right + 1) 범위의 리스트 원소를 변경해준다.  
    0 일때 1, 1 일때, 0
6.  20개씩 출력하는 것은 아래와 같이 for 문에서 조절해주면 된다.
    ```python
    for i in range(1, n, 20):
        print(*switch[i:i+20])
    ```

<br>

## 🖥 소스 코드

```python
from sys import stdin

n = int(stdin.readline())
switch = [0] + list(map(int, stdin.readline().split()))

for i in range(int(stdin.readline())):
    g, num = map(int, stdin.readline().split())

    if g == 1:
        for i in range(num, n + 1, num):
            switch[i] = 1 if switch[i] == 0 else 0

    elif g == 2:
        if num + 1 > n or num - 1 < 1:
            switch[num] = 1 if switch[num] == 0 else 0
        else:
            if switch[num + 1] == switch[num - 1]:
                left = num - 1
                right = num + 1

                while 1:
                    if left - 1 < 1 or right + 1 > n:
                        break

                    if switch[left - 1] != switch[right + 1]:
                        break

                    else:
                        left -= 1
                        right += 1

                for i in range(left, right + 1):
                    switch[i] = 1 if switch[i] == 0 else 0
            else:
                switch[num] = 1 if switch[num] == 0 else 0


for i in range(1, n, 20):
    print(*switch[i:i+20])
```

<br>

## 💾 느낀점

1.  조건문만 충실히 지키면 잘 풀 수 있는 문제였다.
2.  여학생이 바꾸는 스위치들의 조건을 구현하는데에 살짝 힘이 들뻔했다.
3.  링크드리스트로 풀수 있을 것 같다는 생각을 했다.
4.  다음번에는 링크드 리스트로 구현하는 연습을 해보아야겠다.