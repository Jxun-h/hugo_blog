---
author: ["Jxun-h"]
title: "[Programmers] 수식최대화 with Python"
date: "2021-08-29"
description: ""
summary: ""
tags: ["자료구조", "PS", "스택", "알고리즘", "프로그래머스"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---
<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/67257" target="_blank">Programmers - 수식 최대화</a>

<br>

### 💡 조건 및 풀이

1.  계산 가능한 수식이 있는 `expression` 이 주어지며, 길이가 `3이상 100이하`인 문자열.
2.  연산자는 `+, -, *` 만 있다. 피연산자는 `0 이상 999` 이하다.
3.  같은 연산자는 앞에 있는 것이 더 우선순위가 높다.
4.  **연산자의 우선순위를 정해서 그것 먼저 계산해주면 된다.**
5.  계산된 음수는 양수로 바꾸어서 최댓값 계산을 한다.

<br>

### 🔖 예제 및 실행결과

#### 예제

```
expression = "100-200*300-500+20"
expression = "50*6-3*2"
```

#### 실행결과

```
60420
300
```

<br>

### ⌨️ 문제 풀이

1.  답으로 반환할 `answer`를 `-1e9`로 초기화한다.
2.  입력받은 `expression`의 정보를 담을 변수를 하나 만들고,  
    문자열에서 연산자를 구분한 뒤 숫자는 정수형 변수로 변환시켜 각각 리스트에 담는다.
3.  연산자의 우선순위는 `itertools` 의 `permutaions` 를 사용해 순열을 만든 후  
    **set()을 통해 순열의 중복을 없앴다.**
4.  각 순열을 하나씩 for 문으로 꺼내고, 그 순열의 원소를 돌며 최댓값을 계산한다.
5.  **주어지는 문자열의 길이가 매우 길지 않은 점**  
    python 언어의 list와 문자열에 있는 `index()` 함수를 사용.
6.  리스트의 `index()` 함수는 찾고자 하는 데이터의 가장 앞에 있는 것을 반환  
    그렇기 때문에 **같은 연산자인 경우 우선순위가 앞에 있다는 점을 만족**한다
7.  해당하는 인덱스의 연산자 앞 뒤의 숫자를 연산자에 맞게 계산 후,  
    계산한 연산자와 피연산자를 뺀 자리에 계산값을 넣음
8.  반복하여 1개 남은 원소 즉, 수식의 최종 계산값을 `answer` 와 비교해 큰 값으로 교체해주면 된다.  
    뮬론 음수는 `abs()` 함수를 사용해 양수로 변경해주었다.

<br>

### 🖥 소스 코드
```python
from itertools import permutations as pt


def solution(expression):
    answer = -1e9
    op, nums = [], []
    a, b = -1, -1
    new_ex = []

    for i in range(len(expression)):
        if expression[i].isnumeric():
            if a < 0:
                a = i
            else:
                b = i
        else:
            if b < 0:
                b = a

            op.append(expression[i])
            nums.append((a, b))
            new_ex.append(int(expression[a:b+1]))
            new_ex.append(expression[i])
            a, b = -1, -1
    if b > -1:
        new_ex.append(int(expression[a:b+1]))
    else:
        new_ex.append(int(expression[a]))

    k = list(set(op))
    for case in list(set(pt(k, len(k)))):
        temp_new_ex = new_ex[:]
        for j in case:
            while j in temp_new_ex:
                idx = temp_new_ex.index(j)
                if j == '*':
                    temp = temp_new_ex[idx - 1] * temp_new_ex[idx + 1]
                elif j == '-':
                    temp = temp_new_ex[idx - 1] - temp_new_ex[idx + 1]
                else:
                    temp = temp_new_ex[idx - 1] + temp_new_ex[idx + 1]

                temp_new_ex = temp_new_ex[:idx - 1] + [temp] + temp_new_ex[idx + 2:]
        answer = max(answer, abs(temp_new_ex[0]))

    return answer
```

<br>


## 💾 느낀점
-   정규표현식으로 연산자와 피연산자를 구분하여 추출해서 풀면,  
    시간복잡도가 더 줄 수도 있을 것 같다.
-   정규표현식을 더 공부하고 연습해보아야겠다.
-   이보다 expression의 길이가 더 길어 시간초과가 날 때는 어떻게 할 것인지  
    연산을 더 줄일 수 있는 방법을 생각해봐야겠다.
-   괄호를 넣어 eval() 함수를 사용하는 것도 생각해보았는데, 실행 속도에서 생각해보니  
    그리 좋지 않은 풀이 방법인 것 같아 사용하지 않았다.