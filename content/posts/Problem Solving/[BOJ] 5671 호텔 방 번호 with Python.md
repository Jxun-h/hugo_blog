---
author: ["Jxun-h"]
title: "[BOJ] 5671 호텔 방 번호 with Python"
date: "2022-03-18"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/5671" target="_blank">BOJ 5671 호텔 방 번호</a>

<br>

### 💡 조건

1.  선영이는 투숙객에게 불운이 찾아오는 것을 피하기 위해서 반복되는 숫자가 없게 방 번호를 만들려고 한다.
2.  정부는 선영이의 호텔 방 번호는 N보다 크거나 같고, M보다 작거나 같아야 한다는 조건을 걸고 신축 허가를 내주었다.
3.  선영이의 새 호텔에는 방이 최대 몇 개 있을 수 있을까?  
    두 방이 같은 방 번호를 사용할 수 없다
4.  **입력은 여러 개의 테스트 케이스로 이루어져 있고**, 한 줄이다.  
    각 줄에는 문제의 설명에 나와있는 N과 M이 주어진다. (1 ≤ N ≤ M ≤ 5000)
5.  각각의 테스트 케이스에 대해서 N보다 크거나 같고, M보다 작거나 같은 수 중에서 반복되는 숫자가 없는 것의 개수를 출력한다.
6.  **브루트포스 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
87 104
989 1022
22 25
1234 1234
```

#### 실행결과

```py
14
0
3
1
```

<br>

### ⌨️ 문제 풀이

1.  여러개의 테스트 케이스가 있다고 했으니, while로 반복을 하도록 하자.  
    입력받은 테스트케이스가 만약 비어있다면, break로 반목문을 중단해주면 된다.
2.  n 부터 m까지 순회하면서, 각 숫자를 str() 로 변환한 후, set()으로 감싸주면 중복제거가 된다.
3.  (2)번의 결과와 순회하고 있는 숫자의 길이를 비교해 같을 경우에만 res + 1을 해준다.
4.  순회가 끝이 났다면 res를 출력해준다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

while 1:
    data = stdin.readline().rstrip()
    if not data:
        break
    res = 0
    a, b = data.split()
    for i in range(int(a), int(b) + 1):
        if len(set(str(i))) == len(str(i)):
            res += 1
    print(res)
```

<br>

### 💾 느낀점