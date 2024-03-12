---
author: ["Jxun-h"]
title: "[BOJ] 11508 2+1 세일 with Python"
date: "2022-05-09"
description: ""
summary: ""
tags: ["자료구조", "PS", "정렬", "그리디", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/11508" target="_blank">BOJ 11508 2+1 세일</a>

<br>

### 💡 조건

1.  유제품 3개를 한 번에 산다면 그중에서 가장 싼 것은 무료로 지불하고 나머지 두 개의 제품 가격만 지불하면 됩니다.
2.  한 번에 3개의 유제품을 사지 않는다면 할인 없이 정가를 지불해야 합니다.
3.  유제품의 수 N (1 ≤ N ≤ 100,000)
4.  N개의 줄에는 각 유제품의 가격 Ci (1 ≤ Ci ≤ 100,000)  
    정답은 231-1보다 작거나 같다.
5.  최소비용으로 유제품을 구입할 수 있도록 도와주는 문제.
6.  **그리디, 정렬 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
4
3
2
3
2
```

#### 실행결과

```py
8
```

<br>

### ⌨️ 문제 풀이

1.  유제품의 가격을 arr 배열에 입력 받는다.
2.  arr 리스트를 역순으로 정렬(내림차순)한다.
3.  역순으로 정렬된 arr 리스트를 순회하면서 어떤 조건에 해당하지 않으면 ans 에 arr[i]을 추가해줄 것 이다.
4.  (3)에서 말한 조건 >> 가장 비싼 물건 순으로 꾸러미에 넣으면, 최소한 세번째로 비싼 물건을 무료가 될 수 있다.
5.  그렇기 때문에 i 를 mod 3 연산을 해주어 이미 상품 두 개를 꾸러미에 넣었다면, 세번째는 무료이기 때문에 ans에 값을 더해주지 않아도 된다는 것.

<br>

### 🖥 소스 코드

```py
from sys import stdin

arr = []
n = int(stdin.readline())
for i in range(n):
    arr.append(int(stdin.readline()))

arr.sort(reverse=True)
ans = 0

for i in range(n):
    if i % 3 != 2:
        ans += arr[i]
print(ans)
```

<br>

### 💾 느낀점

1.  단순 그리디 문제였는데, 잘 풀지 못했다.
2.  그리디 알고리즘이 묻어(?)있는 유형의 문제들을 매우 고전하는 모습이 보인다.
3.  경우의 수 문제도 헷갈리는데, 생각난 김에 복습을 해봐야할 것 같다.