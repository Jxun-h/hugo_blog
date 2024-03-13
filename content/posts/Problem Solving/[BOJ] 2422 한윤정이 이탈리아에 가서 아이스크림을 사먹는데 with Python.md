---
author: ["Jxun-h"]
title: "[BOJ] 2422 한윤정이 이탈리아에 가서 아이스크림을 사먹는데 with Python"
date: "2022-02-13"
description: ""
summary: ""
tags: ["자료구조", "PS", "브루트포스", "그래프 이론", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2422" target="_blank">BOJ 2422 한윤정이 이탈리아에 가서 아이스크림을 사먹는데</a>

<br>

### 💡 조건

1.  아이스크림 가게에는 N종류의 아이스크림이 있다.  
    모든 아이스크림은 1부터 N까지 번호가 매겨져있다.  
    어떤 종류의 아이스크림을 함께먹으면, 맛이 아주 형편없어진다.
2.  정수 N과 M이 주어진다. (1 ≤ N ≤ 200, 0 ≤ M ≤ 10,000)  
    N은 아이스크림 종류의 수이고, M은 섞어먹으면 안 되는 조합의 개수이다.
3.  같은 조합은 두 번 이상 나오지 않는다.
4.  **브루트포스 알고리즘, 그래프 이론**유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
5 3
1 2
3 4
1 3
```

#### 실행결과

```py
3
```

<br>

### ⌨️ 문제 풀이

1.  저는 브루트포스 알고리즘 보다 그래프 이론으로 풀이하는게 쉬웠습니다.
2.  그래프로 사용할 nope dict 자료형 변수를 생성합니다.  
    키 값은 각 아이스크림의 번호이며, value는 set()으로 설정했습니다.  
    아이스크림의 번호가 매겨져 있는 ice_cream set() 자료형 변수를 생성합니다.
3.  섞이면 안되는 각 아이스크림의 번호를 입력받아 처리를 해줍니다.  
    a 와 b 가 섞이면 안되는 조합이라면, nope[a]에 b를 넣어주고, nope[b]에 a 를 넣어줍니다.
4.  1번부터 N번까지 아이스크림에서 세가지 조합을 찾아야하기에, combinations 함수를 사용하여 조합을 만들어줍니다.  
    중복방지를 위해서 set()으로 둘러싸주고 순회를 시작합니다.
5.  조합으로 선택된 세 개의 번호를 가진 아이스크림을 nope 자료구조에 키값으로 넣었을 때, 번호가 해당하는 곳에 없다면  
    섞여도 되는 조합이기에 결과를 저장할 res 변수에 +1 을 해줍니다.  
    **dict 자료형에 섞이면 안되는 조합을 양방향으로 저장해두었기에, nope[x] 에서 x의 값은 소스코드마다 달라질 수 있습니다.**
6.  res를 출력합니다.

<br>

### 🖥 소스 코드

```py
from sys import stdin
from itertools import combinations

n, m = map(int, stdin.readline().split())
ice_cream = set(x for x in range(1, n + 1))
nope = {x: set() for x in range(1, n + 1)}

for _ in range(m):
    a, b = map(int, stdin.readline().split())
    nope[a].add(b)
    nope[b].add(a)


res = 0
for comb in list(set(combinations(ice_cream, 3))):
    if comb[1] not in nope[comb[0]] 
    and comb[2] not in nope[comb[0]] 
    and comb[1] not in nope[comb[2]]:
        res += 1

print(res)
```

<br>

### 💾 느낀점

1.  해시맵 자료구조(dict) 를 통해서 문제해결을 할 때 기분이 좋습니다.
2.  브루트포스 알고리즘이라고 되어있는데, 사실 그래프 이론 문제로 들어가야하는게 아닌가 싶습니다.