---
author: ["Jxun-h"]
title: "[BOJ] 20436 ZOAC 3 with Python"
date: "2022-05-17"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "시뮬레이션", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/20436" target="_blank">BOJ 20436 ZOAC 3</a>

<br>

### 💡 조건

1.  독수리 타법이란 양 손의 검지손가락만을 이용해 타자를 치는 타법이다.  
    성우는 한글 자음 쪽 자판은 왼손 검지손가락으로 입력하고, 한글 모음 쪽 자판은 오른손 검지손가락으로 입력한다.
2.  a의 좌표가 (x1, y1)이고, b의 좌표가 (x2, y2)일 때,  
    a에 위치한 성우의 손가락이 b로 이동하는 데에는 a와 b의 택시 거리 |x1-x2|+|y1-y2| 만큼의 시간이 걸린다.
3.  각 키를 누르는 데에는 1의 시간이 걸린다.
4.  성우는 두 손을 동시에 움직일 수 없다.  
    성우가 사용하는 키보드는 쿼티식 키보드이며, 아래 그림처럼 생겼다.

<br>
<center><img src='/20436.png'/></center>
<br>

5.  첫 번째 줄에는 두 알파벳 소문자 sL, sR이 주어진다. sL, sR은 각각 왼손 검지손가락, 오른손 검지손가락의 처음 위치이다.  
    그 다음 줄에는 알파벳 소문자로 구성된 문자열이 주어진다. 문자열의 길이는 최대 100자이다. 빈 문자열은 주어지지 않는다.  
    입력으로 주어진 문자열을 출력하는 데에 걸리는 시간의 최솟값을 출력한다.
6.  **구현, 시뮬레이션** 유형의 문제
7.  성우가 두 손을 동시에 움직이지 못하는 이유는 다음과 같다.
    1.  사람은 두 가지 이상의 일을 동시에 할 수 없다.
    2.  대학원생은 사람이다.
    3.  성우는 대학원생이다.

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
z o
zoac
```

#### 실행결과

```py
8
```

<br>

### ⌨️ 문제 풀이

1.  문제에 **한글 자음 쪽 자판은 왼손 검지손가락으로 입력하고, 한글 모음 쪽 자판은 오른손 검지손가락으로 입력한다.**  
    라는 문구가 있다. 이는 자음과 모음을 따로 구분하여 구현을 하는 것이 좋을 것이라는 힌트를 얻을 수 있다.
2.  키보드가 생긴 모양을 따라 keyboard 리스트를 생성하고, 모음을 따로 분리하여 모음 리스트를 생성한다면, 아래와 같이 만들 수 있다.
3.  `keyboard = ['qwertyuiop', 'asdfghjkl', 'zxcvbnm'] mo = 'yuiophjklbnm'`
4.  첫번째 줄에 주어진 손이 위치한 알파벳을 입력받아, 손 위치의 좌표를 저장한다.
5.  각 문자마다 누르는 시간은 1만큼 소요되기 때문에, 입력하려고 하는 문자열을 순회하면서 ans + 1을 해준다.
6.  입력하려는 문자 s 가 모음 리스트에 있을 때, 오른손에 해당하는 좌표로부터 누르려는 키까지의 거리를 계산하여 ans에 더해준다.
7.  입력하려는 문자 s 가 모음 리스트에 없을 때, 왼손에 해당하는 좌표로부터 누르려는 키까지의 거리를 계산하여 ans에 더해준다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

l, r = map(str, stdin.readline().rstrip().split())
string = stdin.readline().rstrip()

keyboard = ['qwertyuiop', 'asdfghjkl', 'zxcvbnm']
mo = 'yuiophjklbnm'
xl, yl, xr, yr = None, None, None, None

for i in range(len(keyboard)):
    if l in keyboard[i]:
        xl, yl = i, keyboard[i].index(l)

    if r in keyboard[i]:
        xr, yr = i, keyboard[i].index(r)

ans = 0
for s in string:
    ans += 1
    if s in mo:
        for i in range(len(keyboard)):
            if s in keyboard[i]:
                nx = i
                ny = keyboard[i].index(s)

                ans += abs(xr - nx) + abs(yr - ny)

                xr, yr = nx, ny
                break

    else:
        for i in range(len(keyboard)):
            if s in keyboard[i]:
                nx = i
                ny = keyboard[i].index(s)

                ans += abs(xl - nx) + abs(yl - ny)

                xl, yl = nx, ny
                break

print(ans)
```
