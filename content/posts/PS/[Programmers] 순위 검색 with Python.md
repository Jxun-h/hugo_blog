---
author: ["Jxun-h"]
title: "[Programmers] 순위 검색 with Python"
date: "2021-10-14"
description: ""
summary: ""
tags: ["이분탐색", "PS", "자료구조", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/72412" target="_blank">Programmers - 순위 검색</a>

<br>

### 💡 조건 및 풀이

1.  **조건**을 만족하는 사람 중 `코딩테스트 점수를 X점 이상 받은 사람`은 모두 몇 명인가?  
    를 구하는 문제
2.  `'-'` 표시는 해당 조건을 고려하지 않겠다는 의미.
3.  ```python
    "cpp and - and senior and pizza 500"
    ```
    
    은를 의미한다.
4.  `"cpp로 코딩테스트를 봤으며, 경력은 senior 이면서 소울푸드로 pizza를 선택한 지원자 중 코딩테스트 점수를 500점 이상 받은 사람은 모두 몇 명인가?"`
5.  **브루트포스 알고리즘 유형의 문제에 해당한다.**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
info = ["java backend junior pizza 150", "python frontend senior chicken 210", "python frontend senior chicken 150","cpp backend senior pizza 260", "java backend junior chicken 80", "python backend senior chicken 50"]

query = ["java and backend and junior and pizza 100", "python and frontend and senior and chicken 200", "cpp and - and senior and pizza 250", "- and backend and senior and - 150", "- and - and - and chicken 100", "- and - and - and - 150"]
```

#### 실행결과

```python
[1,1,1,1,2,4]
```

<br>

### ⌨️ 문제 풀이

1.  info 배열을 순회하며 얻은 데이터를 잘라 배열로 만들고, 그 배열을 각각 데이터와 점수 부분으로 나누어 준다.
2.  `temp = j.split() condition = temp[:-1] score = int(temp[-1])`
3.  지원서에 입력한 4개의 값 range(4)의 데이터를 combinations 을 이용해  
    짝을 지어 각 1부터 4개까지의 경우의 수와 점수를 dict 자료구조에 넣어준다.
4.  `for i in range(5): comb = list(combinations(range(4), i)) for c in comb: test_case = condition.copy() for idx in c: test_case[idx] = '-' case = ''.join(test_case) if case not in data: data[case] = [score] else: data[case].append(score)`
5.  이분탐색 라이브러리인 bisect 라이브러리를 사용해 사용을 할 것이기 때문에 dict 자료구조의 value를 정렬해준다.
6.  파라미터로 받아온 sql을 순차적으로 돌면서 and 문자열을 ''로 바꾸어주고 split 해준다.  
    test\_query 와 test\_score 로 나누어주고, test\_query에 해당하는 인원 중(data의 key)  
    test\_score 이상의 점수를 얻은(data의 value) 인원의 수를 계산하여 answer에 입력해준다.

<br>

### 🖥 소스 코드

```python
from itertools import combinations
from bisect import bisect_left


def solution(info, query):
    answer, data, sql = [], {}, []

    n, m = len(info), len(query)

    for j in info:
        temp = j.split()
        condition = temp[:-1]
        score = int(temp[-1])

        for i in range(5):
            comb = list(combinations(range(4), i))
            for c in comb:
                test_case = condition.copy()
                for idx in c:
                    test_case[idx] = '-'
                case = ''.join(test_case)
                if case not in data:
                    data[case] = [score]
                else:
                    data[case].append(score)
    for i in data.values():
        i.sort()

    for i in range(m):
        sql = query[i].replace('and', '').split()
        test_query = ''.join(sql[:-1])
        test_score = int(sql[-1])

        if test_query in data:
            idx = bisect_left(data[test_query], test_score)
            answer.append(len(data[test_query]) - idx)
        else:
            answer.append(0)

    return answer
```

<br>

### 💾 느낀점

-   모든 경우의 수를 data 에 입력하여 찾는 아이디어를 구상하는 것이 힘이 들었다.
-   sql에 해당하는 지원자를 이분탐색으로 찾을 아이디어와 dict 자료구조를 사용할 아이디어를 떠올리니  
    구현하는데에는 큰 무리가 없었던 것 같다.
-   포스팅 내용을 보니 아예 아이디어를 얻지 못한 분들이 보시기에 괜찮을까 라는 생각이 들면서,  
    설명하는 능력이 조금 부족하다고 느낀다.