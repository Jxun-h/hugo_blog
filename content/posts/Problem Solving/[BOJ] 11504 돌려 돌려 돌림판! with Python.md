---
author: ["Jxun-h"]
title: "[BOJ] 11504 돌려 돌려 돌림판! with Python"
date: "2022-01-11"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "시뮬레이션", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/11504" target="_blank">BOJ 11504 돌려 돌려 돌림판!</a>

<br>

### 💡 조건

1.  첫 번째 줄에 테스트케이스의 개수 `T`
2.  테스트케이스의 첫 줄에는 돌림판을 `N`등분할 정수 `N (1 ≤ N ≤ 100)`  
    `X, Y의 길이 M (1 ≤ M ≤ 9, M ≤ N)`  
    다음 3개의 줄에 `X`의 각 자리수, `Y`의 각 자리수, 돌림판의 상태
3.  돌림판에서 `X ≤ Z ≤ Y`를 만족하는 `M`자리의 수 `Z`가 몇 개가 있는 지를 출력
4.  `X`와 `Y`사이에 있는 수가 `123` 밖에 없는 데 돌림판에서 `2`번 나온다면, `1`이 아닌 `2`를 출력
5.  **구현, 시뮬레이션 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3
8 3
2 0 0
3 1 1
3 7 8 3 1 9 2 7
5 2
8 8
9 9
1 3 2 5 4
6 3
0 0 0
9 9 9
1 2 3 4 5 6
```

#### 실행결과

```py
1
0
6
```

<br>

### ⌨️ 문제 풀이

1.  돌림판의 숫자를 입력받아, `m`개의 개수만큼 이어붙여 새로운 숫자를 만든다.
2.  `x` 와 `y` 사이에 있는 숫자인지 확인한 후, `res`를 갱신한다.
3.  res 출력

<br>

### 🖥 소스 코드

```py
from sys import stdin

for _ in range(int(stdin.readline())):
    n, m = map(int, stdin.readline().split())
    x = int(''.join(list(stdin.readline().split())))
    y = int(''.join(list(stdin.readline().split())))
    data = list(map(int, stdin.readline().split()))
    data += data[:m]
    res = 0

    for i in range(n):
        check = int(''.join(map(str, data[i:i+m])))
        if x <= check <= y:
            res += 1

    print(res)
```

<br>

### 💾 느낀점

1.  구현 & 시뮬레이터 문제 중 브론즈인만큼 매우 쉬운 문제.
2.  문제가 길어서 읽기 귀찮아도 막상 읽어보면 별거 아닌 문제.
3.  구현과 시뮬레이션이라기보다, 문제 읽고 압축하는 연습은 됐다고 생각합니다.