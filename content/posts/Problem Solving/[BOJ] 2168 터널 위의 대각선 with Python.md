---
author: ["Jxun-h"]
title: "[BOJ] 2168 터널 위의 대각선 with Python"
date: "2022-02-21"
description: ""
summary: ""
tags: ["자료구조", "PS", "수학", "정수론", "유클리드 호제법", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2168" target="_blank">BOJ 2168 터널 위의 대각선</a>

<br>

### 💡 조건

1.  한 변의 길이가 1cm인 정사각형 모양의 타일이 있다.  
    이 타일들을 가로가 xcm, 세로가 ycm인 직사각형 모양의 벽에 빈틈없이 붙였다. x와 y는 정수이다.
2.  직사각형에 붙어 있는 x*y개의 타일 중에는 대각선이 그려진 타일도 있고, 그렇지 않은 타일도 있다.
3.  x*y개의 타일 중에서 대각선이 그려져 있는 타일의 개수를 구하는 문제.
4.  x와 y는 1,000,000,000 이하의 자연수
5.  **수학, 정수론, 유클리드 호제법**유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
8 12
```

#### 실행결과

```py
16
```

<br>

### ⌨️ 문제 풀이

1.  유클리드 호제법과 관련된 문제입니다.
2.  대각선이 꼭지점을 지나가지 않는 직사각형의 개수는 x + y + 1  
    대각선이 꼭지점을 지나가는 직사각형의 개수는 x + y - (점의 개수) - 1  
    입니다.
3.  점의 개수는 gcd(x, y) - 1개 입니다.
4.  우리는 대각선이 꼭지점을 지나가는 직사각형의 개수를 구해야하기 때문에  
    (2)번의 두번째 공식을 이용해야하며, x + y - gcd(x + y) 가 성립한다.
5.  x + y - gcd(x + y) 를 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from math import gcd
x, y = map(int, stdin.readline().split())
print(x + y - gcd(x, y))
```

<br>

### 💾 느낀점

1.  수학적인 지식이 부족해 어려웠습니다.