---
author: ["Jxun-h"]
title: "[Programmers] 외벽 점검 with Python"
date: "2021-12-06"
description: ""
summary: ""
tags: ["자료구조", "PS", "set", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["Programmers"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/60062" target="_blank">Programmers 외벽 점검 with Python</a>

<br>

### 💡 조건

1.  외벽의 총 둘레길이 `(1 <= n <= 200)`  
    취약 지점의 위치가 담긴 배열 `(1< = weak <= 15)`
    -   서로 다른 두 취약점의 위치가 같을 경우는 없다.
    -   취약지점의 위치는 오름차순이다.
    -   `(0 <= weak의 원소 <= n-1)`
2.  친구가 1시간 동안 이동할 수 있는 거리 `(1<= dist <= 8)`
3.  친구들을 최소한으로 투입시켜서 외벽 점검을 해야한다.  
    만약 친구들이 모두 투입되어도 외벽을 모두 점검할 수 없다면, `-1`을 출력.
4.  **순열, 브루트포스 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
print(solution(12, [1, 5, 6, 10], [1, 2, 3, 4], 2))
```

#### 실행결과

```python
2
```

<br>

### ⌨️ 문제 풀이

1.  점검 해야할 외벽의 길이를 구하기 위해 `weak`의 길이를 `leng` 이라는 변수에 담아준다.
2.  총 `n` 만큼의 외벽이 있으니, `weak` 의 길이만큼 순회하면서 `weak` 의 원소에 n을 더하여  
    **원형 모양의 외벽을 펼쳐준다**고 생각하자.
3.  `answer`의 값은 점검을 투입할 수 있는 친구들의 수(`dist`의 길이)보다 `1` 많게 저장한다.  
    이 과정이 있어야 모두 투입시켜도 안될 때 `-1`을 출력하게 할 수 있다.
4.  취약점 어디서부터 시작할지에 따라서 인원의 수가 적어질 수도, 많아질 수도 있다.  
    그렇기 때문에 `start(출발지점)` 을 `weak`의 길이만큼 순회시켜 돌게하고,
5.  친구들이 투입될 순서는 `permutations` 함수를 통해 변경한다.

5.  `count = 0`으로 초기화 한 뒤, `position`을 정한다.  
    취약점 배열에서 `start` 번째에서  
    친구들의 1시간동안 이동거리를 `permutations`로 뽑아낸 배열의 `count - 1` 번째의 값을  
    빼준 것이 `position` 값이다.
6.  그렇다면, `취약점 시작부분(start)` 부터 `취약점 시작부분(start) + 취약점의 개수(leng)`까지 순회하면서`(index)`  
    현재 포지션 값이 취약점배열의 `index`에 해당하는 값보다 작다면 `count += 1` 을 해준다.  
    `count` 가 혹시 친구의 수를 넘었다면 바로 중단한다.  
    그게 아니라면 작업을 한 후, `position을 갱신`한다.
7.  `answer` 와 `count` 중에 가장 작은 것을 `answer`에 담아 갱신한 뒤, `answer`가 `dist의 길이`보다 크다면 `-1을 반환`하고  
    그게 아니라면 `answer를 반환`한다.

<br>

### 🖥 소스 코드

```python
from itertools import permutations


def solution(n, weak, dist):
    leng = len(weak)
    for x in range(leng):
        weak.append(weak[x] + n)

    answer = len(dist) + 1

    for start in range(leng):
        for friends in list(permutations(dist, len(dist))):
            count = 0
            position = weak[start] - friends[count - 1]

            for index in range(start, start + leng):
                if position < weak[index]:
                    count += 1
                    if count > len(dist):
                        break
                    position = weak[index] + friends[count - 1]
            answer = min(answer, count)
    if answer > len(dist):
        return -1

    return answer
```

<br>

### 💾 느낀점

1.  외벽을 평면으로 펼칠 아이디어를 떠올리지 못하고 해설을 본 후 큰 충격을 받았다.
2.  이후, 외벽 점점을 해야할 취약점 중 한 부분을 골라 취약점의 길이만큼 점검하는 로직을 구현하는데에  
    많은 노력과 긴 시간이 필요했다.
3.  스스로 구현이 약하다는 것을 알고 있다. 조금 더 구현할 때 그림을 그리긋 설계하고, 짧아도 구현계획을 써내려가야겠다.
4.  스스로 검증하는 부분에서 큰 약점이 있다는 것을 느꼈다.