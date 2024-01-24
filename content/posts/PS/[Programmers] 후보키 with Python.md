---
author: ["Jxun-h"]
title: "[Programmers] 후보키 with Python"
date: "2021-11-27"
description: ""
summary: ""
tags: ["자료구조", "PS", "set", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["Programmers"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/42890" target="_blank">Programmers 후보키 with Python</a>

<br>

### 💡 조건

1.  relation 은 2차원 문자열 배열이다.  
    `1 <= relation 의 컬럼의 길이 <= 8`  
    `1 <= relation 의 로우의 길이 <= 20`  
    `1 <= relation 의 모든 문자열의 길이 <= 8, 알파벳 소문자와 숫자로만 이루어져 있다.`  
    **`중복되는 튜플은 없다.`**
2.  학생들의 인적사항이 주어졌을 때, **후보 키의 최대 개수**를 구하라.  
    즉, 학생들을 구별할 수 있는 **유일성과 최소성을 지키는 키의 조합의 개수**를 구하면 된다.
3.  **조합의 개수를 구하는 문제**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
[["100","ryan","music","2"],["200","apeach","math","2"],["300","tube","computer","3"],["400","con","computer","4"],["500","muzi","music","3"],["600","apeach","music","2"]]
```

#### 실행결과

```python
2
```

<br>

### ⌨️ 문제 풀이

1.  `row`와 `column` 의 개수를 구해 변수로 둔다.  
    키값이 될 수 있는 1개부터 `column` 의 길이의 조합을 각각 구해서 `candidates`에 저장한다.
2.  1번에서 구한 조합의 경우의 수를 순회하면서 해당되는 `relation` 의 데이터를 `tmp` 에 저장한 후  
    `set()` 으로 자료형을 변경하여 중복을 제거한 후, `row의 개수`와 비교한다.  
    만약 같다면, 후보키가 될 수 있는 것이기에 `unique` 변수에 저장한다  
    **추출한 데이터가 유일성을 가지는지에 대해서 검사하는 것.**

3.  `answer` 변수에 3번 작업을 통해 나온 `unique` 변수에 있는 데이터를 `set()` 자료형으로 중복을 제거한 뒤 저장한다.  
    `unique` 변수의 길이만큼 순회하면서 **(i)**  
    `i` 이후의 각 키조합에 **(j)** `i`가 포함이 되어 있다면, answer에서 `j`를 제거한다.  
    `i`가 `j`에 포함이 된다면, `j`는 원소 하나가 빠져도 `최소성`을 만족하지 않기에 제거하는 것.
4.  `answer`의 길이를 반환

<br>

### 🖥 소스 코드

```python
from itertools import combinations


def solution(relation):
    col = len(relation[0])
    row = len(relation)

    candidates = []

    for i in range(1, col + 1):
        candidates.extend(combinations(range(col), i))

    unique = []
    for candi in candidates:
        tmp = [tuple([item[i] for i in candi]) for item in relation]
        if len(set(tmp)) == row:
            unique.append(candi)

    answer = set(unique)
    for i in range(len(unique)):
        for j in range(i + 1, len(unique)):
            if len(unique[i]) == len(set(unique[i]) & set(unique[j])):
                answer.discard(unique[j])

    return len(answer)
```

<br>

## 💾 느낀점

1.  조합을 사용하여 문제에서 제시한 최소성과 유일성을 이해하고 문제를 풀이해야했다.
2.  주어진 데이터의 길이의 크기가 작아서 완전탐색을 통해서 할 수 있었다.
3.  `set()` 자료구조의 성질을 통해서 중복을 제거할 수 있다는 것을 알고 있다면 더 편하게 풀 수 있는 문제였다.