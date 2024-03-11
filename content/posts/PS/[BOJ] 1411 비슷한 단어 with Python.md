---
author: ["Jxun-h"]
title: "[BOJ] 1411 비슷한 단어 with Python"
date: "2021-12-12"
description: ""
summary: ""
tags: ["자료구조", "PS", "그리디", "브루트포스", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1411" target="_blank">BOJ 1411 비슷한 단어</a>

### 💡 조건

1.  문자열 A를 숌스럽게 바꾸어 B로 만들었다면, 그 단어는 비슷한 단어라고한다.
2.  숌스럽게 바꾼다는 것은 단어 A에 등장하는 모든 알파벳을 다른 알파벳으로 바꾼다.
3.  단어가 여러 개 주어졌을 때, 몇 개의 쌍이 비슷한지 구하는 문제.
4.  단어의 길이는 최대 50  
    N은 100보다 작거나 같은 자연수이다.  
    모든 단어의 길이는 같고, 중복되지 않는다.
5.  **브루트포스 알고리즘 유형**의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
12
cacccdaabc
cdcccaddbc
dcdddbccad
bdbbbaddcb
bdbcadbbdc
abaadcbbda
babcdabbac
cacdbaccad
dcddabccad
cacccbaadb
bbcdcbcbdd
bcbadcbbca
```

#### 실행결과

```python
13
```

<br>

### ⌨️ 문제 풀이

1.  가능한 각 단어들의 쌍을 combinations 함수를 사용해 만들고 순차적으로 순회한다.
2.  이미 변환했던 단어를 저장할 집합 자료형 use를 생성하고, 단어의 길이만큼 순회하면서 아래의 조건에 해당하는지 확인한다.
    -   순회하고 있는 알파벳이 서로 같지않고, a\[i\]번 째 단어가 사용되지 않고, change에 없다.
3.  2번에 있는 조건이 참일 경우
4.  ```python
    change[a[i]] = b[i] use.add(b[i]) a[i] = b[i]
    ```
5.  2번에 있는 조건이 거짓일 경우, a\[i\]가 change에 있는지 확인한다.
    -   참일 경우, a\[i\] = change\[a\[i\]\]

5.  4번의 조건이 거짓일 경우, a\[i\]가 use에 있는지 확인한다.
    -   있는 경우에 tf를 False로 저장하고, 반복문을 멈춘다.
    -   없는 경우는 아래의 코드를 실행한다.
        
        ```python
        change[a[i]] = b[i]
        use.add(b[i])
        ```
        
6.  순회를 마치면 a와 b가 같은지, tf가 True인지 확인한다.  
    참이면, 문자열 쌍을 배열에 저장한다.
7.  배열의 길이를 출력한다.

<br>

### 🖥 소스 코드

```python
from sys import stdin
from itertools import combinations

words = []
res = set()
tc = int(stdin.readline())

if tc == 1:
    print(res)
else:
    for _ in range(tc):
        words.append(stdin.readline().rstrip())

    for pair in list(set(combinations(words, 2))):
        change = dict()
        use = set()
        tf = True
        x, y = pair
        a, b = pair
        a, b = list(a), list(b)
        n, m = len(a), len(b)

        if n != m:
            continue
        else:
            for i in range(n):
                if a[i] != b[i] and b[i] not in use and a[i] not in change:
                    change[a[i]] = b[i]
                    use.add(b[i])
                    a[i] = b[i]
                else:
                    if a[i] in change:
                        a[i] = change[a[i]]
                    else:
                        if a[i] in use:
                            tf = False
                            break
                        else:
                            change[a[i]] = b[i]
                            use.add(b[i])

            if a == b and tf:
                res.add((x, y))

    print(len(res))
```

<br>

### 💾 느낀점

1.  실버 II 티어의 문제인데, 생각보다 조건이 까다로워서 구현하는데에 애를 먹었다.
2.  생각보다 부르트포스 알고리즘 유형이 풀기 까다롭다는 생각을 하게 된 문제였다