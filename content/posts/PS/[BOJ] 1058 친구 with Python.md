---
author: ["Jxun-h"]
title: "[BOJ] 1058 친구 with Python"
date: "2022-02-01"
description: ""
summary: ""
tags: ["자료구조", "PS", "플로이드 와샬", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1058" target="_blank">BOJ 1058 친구</a>

<br>

### 💡 조건

1.  어떤 사람 A가 또다른 사람 B의 2-친구가 되기 위해선, 두 사람이 친구이거나, A와 친구이고, B와 친구인 C가 존재해야 된다.
2.  여기서 가장 유명한 사람은 2-친구의 수가 가장 많은 사람이다. 가장 유명한 사람의 2-친구의 수를 출력하는 프로그램을 작성하시오.
3.  **A와 B가 친구면, B와 A도 친구이고, A와 A는 친구가 아니다.**
4.  사람의 수 N이 주어진다. N은 50보다 작거나 같은 자연수이다.  
    둘째 줄부터 N개의 줄에 각 사람이 친구이면 Y, 아니면 N이 주어진다.  
    가장 유명한 사람의 2-친구의 수를 출력한다.
5.  **플로이드-와샬 알고리즘 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
10
NNNNYNNNNN
NNNNYNYYNN
NNNYYYNNNN
NNYNNNNNNN
YYYNNNNNNY
NNYNNNNNYN
NYNNNNNYNN
NYNNNNYNNN
NNNNNYNNNN
NNNNYNNNNN
```

#### 실행결과

```py
8
```

<br>

### ⌨️ 문제 풀이

1.  플로이드-와샬 알고리즘 알고리즘을 사용하여 문제를 풀이한다.
2.  Y를 1로, N을 0으로 변환한 뒤, arr에 입력받은 데이터를 저장한다.
3.  test 배열에 arr배열을 복사한 뒤, 플로이드-와샬 알고리즘을 돌리기 위한 3중 반복문을 순회한다.
4.  arr\[i\]\[k\] 와 arr\[k\]\[j\] 가 1이라면, test\[i\]\[j\]에 1을 저장한다.  
    i와 j 가 한다리 건너서 친구인지 확인하는 구간이다.
5.  test 배열을 순회하면서 test\[i\]의 합이 최댓값인 것을 찾아서 결과값을 저장할 res 변수에 저장하고, 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
arr = []
for i in range(n):
    temp = stdin.readline().rstrip().replace("N", '0').replace("Y", '1')
    data = list(map(int, list(temp)))
    arr.append(data)

res = [0] * n
test = [item[:] for item in arr]

for k in range(n):
    for i in range(n):
        for j in range(n):
            if i != j:
                if arr[i][k] and arr[k][j]:
                    test[i][j] = 1

res = 0
for i in range(n):
    friends = sum(test[i])
    if res < friends:
        res = friends

print(res)
```

<br>

### 💾 느낀점

1.  플로이드-와샬 알고리즘의 응용문제였다.
2.  모든 노드에서의 최단거리를 찾는 방식이 아닌,  
    모든 노드에서 친구가 될 수 있는 경우를 찾아 test 배열에 저장하는 방식으로 풀이했다.

