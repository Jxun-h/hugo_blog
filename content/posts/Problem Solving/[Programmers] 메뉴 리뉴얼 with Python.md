---
author: ["Jxun-h"]
title: "[Programmers] 메뉴 리뉴얼 with Python"
date: "2021-10-13"
description: ""
summary: ""
tags: ["정렬", "PS", "구현", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["Programmers"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/72411" target="_blank">Programmers - 메뉴 리뉴얼</a>

<br>

### 💡 조건 및 풀이

1.  `orders` 배열의 크기는 2 이상 20 이하.
2.  `orders` 배열의 각 원소는 크기가 2 이상 10 이하인 문자열.  
    각 문자열은 알파벳 대문자로만 이루어져 있으며 **중복은 허용 안함.**
3.  `course` 배열의 크기는 1 이상 10 이하.  
    `course` 배열의 각 원소는 2 이상 10 이하인 자연수가 오름차순으로 정렬
4.  정답은 각 코스요리 메뉴의 구성을 **문자열 형식으로 배열에 담아 사전 순으로 오름차순 정렬**해서 return  
    배열의 각 원소에 저장된 문자열 또한 알파벳 **오름차순**으로 정렬  
    만약 **가장 많이 함께 주문된 메뉴 구성이 여러 개라면, 모두 배열에 담아 return**  
    **무조건 `return 하는 배열의 길이가 1 이상`**
5.  **Python 조합`(combinations)` 라이브러리를 사용해 구현**  
    dict를 사용해도 되는 문제.  
    정렬이 중요한 문제.
6.  **각 손님은 단품메뉴를 2개 이상 주문해야 한다.**
7.  **최소 2명 이상의 손님으로부터 주문**된 **단품메뉴 조합**에 대해서만 코스요리 메뉴 후보에 포함

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
print(solution(["ABCFG", "AC", "CDE", "ACDE", "BCFG", "ACDEH"], [2, 3, 4]))
```

#### 실행결과

```python
["AC", "ACDE", "BCFG", "CDE"]
```

<br>

### ⌨️ 문제 풀이

1.  주문을 받은 `orders` 배열을 순차적으로 순회할 반복문.
2.  순회하며 메뉴들을 리스트로 만들어 정렬.
3.  코스를 만들 메뉴 개수를 순회할 반복문. << 여기까지 2중 반복문. `j`
4.  `조합 라이브러리`를 사용해 3번 반복문에서 나오는 코스의 메뉴개수만큼 메뉴를 뽑아서  
    중복을 없앤 뒤 t문자열에 저장. **(t는 j 개를 뽑아 만든 메뉴의 조합입니다.)**
    
    ```python
    list(set(combinations(data, j)))
    # set()은 중복을 없애줍니다!
    ```
    
5.  `t` 가 점수판에 없으면 새로 등록시켜 **1점 부여**  
    `t` 가 점수판에 있으면 **1점 부여**
6.  **최소 2명 이상의 손님으로부터 주문**된 **단품메뉴 조합** 만 해당하기 때문에  
    `score`에 저장된 점수가 1점 이상이라면 `new_score`에 `(메뉴, 점수)` 형식으로 저장 후 점수를 기준으로 정렬
    
    ```python
    """
    # lambda 설명
    x 를 x[1] 기준으로 정렬할건데, -가 붙으면 역순입니다.
    """ 
    new_score.sort(key=lambda x: -x[1])
    ```
    
7.  마지막으로 코스요리를 구성할 메뉴 개수를 순회하면서 `new_score`에 넣은 코스메뉴 후보들을 검사하면서  
    정답으로 반환할 배열 `answer`에 넣어주고, **정렬을 한 뒤 반환 시켜준다.**

<br>

### 🖥 소스 코드

```python
from itertools import combinations


def solution(orders, course):
    answer = []
    score = {}
    n = len(orders)
    for i in range(n):
        data = sorted(list(orders[i]))
        for j in course:
            for k in list(set(combinations(data, j))):
                t = ''.join(k)
                if t in score:
                    score[t] += 1
                else:
                    score[t] = 1

    new_score = []
    for menu, num in score.items():
        if num > 1:
            new_score.append((menu, num))

    new_score.sort(key=lambda x: -x[1])

    for i in course:
        max_order = 0
        for c, num in new_score:
            if len(c) == i:
                if max_order <= num:
                    max_order = num
                    answer.append(c)
                else:
                    break
    answer.sort()
    return answer
```

<br>

### 💾 느낀점

-   정렬을 할 때 `lambda`를 많이 사용한게 도움이 되었다.
-   `combinations`를 사용해서 번거로운 일이 적어서 좋았다.  
    이런 간편한 라이브러리를 알고 있다는 것보다 사용할 때를 알고 있다는게 기분 좋았다.
-   카카오 기춟문제는 문제도 길고 조건도 자세하게 써있는데 눈에 잘 안들어온다.  
    아직 문제 압축능력이 부족한 것 같다.