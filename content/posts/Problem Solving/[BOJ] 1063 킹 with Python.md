---
author: ["Jxun-h"]
title: "[BOJ] 1063 킹 with Python"
date: "2021-12-29"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "시뮬레이션", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1063" target="_blank">BOJ 1063 킹</a>

<br>

### 💡 조건

1.  체스판의 크기는 8*8
2.  체스판에서의 말의 위치는 알파벳 하나와 숫자 하나로 구성되어 있다.  
    알파벳은 열(column), 숫자는 행(row)을 상징한다.  
    알파벳은 A
    
    ~H, 숫자는 1~
    
    8까지이다.
3.  킹이 움직일 수 있는 방법은 8가지가 있으며, 문제에 제시되어 있다.
4.  체스판에 있는 돌은 킹이 움직인 방향으로 같이 움직인다.  
    체스판이나 돌이 입력에서 주어진대로 움직이다가 밖으로 나갈 경우, 그 이동은 건너 뛴다.
5.  첫째 줄에 킹의 마지막 위치, 둘째 줄에 돌의 마지막 위치를 출력한다.
6.  **구현, 시뮬레이션**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
A1 A2 5
B
L
LB
RB
LT
```

#### 실행결과

```py
A1
A2
```

<br>

### ⌨️ 문제 풀이

1.  첫 위치를 입력 받고, 주어진 입력의 횟수만큼 이동명령을 받아 처리하면 된다.
    -   대문자 A~H 는 아스키 코드 숫자를 사용하여 처리를 하는 것이 훨씬 편하다.
2.  각 커맨드마다 움직이는 좌표를 수정해주면서 아래의 확인사항을 체크한다.
    -   킹은 움직이지 못하는데 돌이 움직일 수 있는 경우는 그냥 넘어간다.
    -   돌은 움직이지 못하는데 킹이 움직일 수 있는 경우는 그냥 넘어간다.
    -   움직이지 못하는 곳이라면 가볍게 무시하고 다음으로 넘어간다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

k, s, n = stdin.readline().rstrip().split()
pos_k = [ord(k[0]), int(k[1])]
pos_s = [ord(s[0]), int(s[1])]

for _ in range(int(n)):
    com = stdin.readline().rstrip()
    if com == 'R':
        if 64 < pos_k[0] + 1 < 73:
            pos_k[0] += 1

            if pos_k == pos_s:
                if 64 < pos_s[0] + 1 < 73:
                    pos_s[0] += 1
                else:
                    pos_k[0] -= 1

    elif com == 'L':
        if 64 < pos_k[0] - 1 < 73:
            pos_k[0] -= 1

            if pos_k == pos_s:
                if 64 < pos_s[0] - 1 < 73:
                    pos_s[0] -= 1
                else:
                    pos_k[0] += 1

    elif com == 'B':
        if 0 < pos_k[1] - 1 < 9:
            pos_k[1] -= 1

            if pos_k == pos_s:
                if 0 < pos_s[1] - 1 < 9:
                    pos_s[1] -= 1
                else:
                    pos_k[1] += 1

    elif com == 'T':
        if 0 < pos_k[1] + 1 < 9:
            pos_k[1] += 1

            if pos_k == pos_s:
                if 0 < pos_s[1] + 1 < 9:
                    pos_s[1] += 1
                else:
                    pos_k[1] -= 1

    elif com == 'RT':
        if 0 < pos_k[1] + 1 < 9 and 64 < pos_k[0] + 1 < 73:
            pos_k[0] += 1
            pos_k[1] += 1

            if pos_k == pos_s:
                if 0 < pos_s[1] + 1 < 9 and 64 < pos_s[0] + 1 < 73:
                    pos_s[0] += 1
                    pos_s[1] += 1
                else:
                    pos_k[0] -= 1
                    pos_k[1] -= 1

    elif com == 'LT':
        if 0 < pos_k[1] + 1 < 9 and 64 < pos_k[0] - 1 < 73:
            pos_k[0] -= 1
            pos_k[1] += 1

            if pos_k == pos_s:
                if 0 < pos_s[1] + 1 < 9 and 64 < pos_s[0] - 1 < 73:
                    pos_s[0] -= 1
                    pos_s[1] += 1
                else:
                    pos_k[0] += 1
                    pos_k[1] -= 1

    elif com == 'RB':
        if 0 < pos_k[1] - 1 < 9 and 64 < pos_k[0] + 1 < 73:
            pos_k[0] += 1
            pos_k[1] -= 1

            if pos_k == pos_s:
                if 0 < pos_s[1] - 1 < 9 and 64 < pos_s[0] + 1 < 73:
                    pos_s[0] += 1
                    pos_s[1] -= 1
                else:
                    pos_k[0] -= 1
                    pos_k[1] += 1

    elif com == 'LB':
        if 0 < pos_k[1] - 1 < 9 and 64 < pos_k[0] - 1 < 73:
            pos_k[0] -= 1
            pos_k[1] -= 1

            if pos_k == pos_s:
                if 0 < pos_s[1] - 1 < 9 and 64 < pos_s[0] - 1 < 73:
                    pos_s[0] -= 1
                    pos_s[1] -= 1
                else:
                    pos_k[0] += 1
                    pos_k[1] += 1


print('{}'.format(chr(pos_k[0]) + str(pos_k[1])))
print('{}'.format(chr(pos_s[0]) + str(pos_s[1])))
```

<br>

### 💾 느낀점

1.  위치를 저장하는 알파벳과, 숫자를 계산하여 상태를 저장하면 되는 문제였다.
2.  열과 행에 해당하는 알파벳과 숫자를 핸들링하여 상태가 변화할 때 가능한 움직임인지 체크하는 부분이 확실히 헷갈리고 어려웠다.