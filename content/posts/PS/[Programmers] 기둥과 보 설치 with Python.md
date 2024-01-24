---
author: ["Jxun-h"]
title: "[Programmers] 기둥과 보 설치 with Python"
date: "2021-11-28"
description: ""
summary: ""
tags: ["구현", "PS", "시뮬레이션", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["Programmers"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/60061" target="_blank">Programmers 기둥과 보 설치 with Python</a>

<br>

### 💡 조건

1.  `5 <= n <= 100`  
    `1 <= 입력받을 기둥과 보의 개수 <= 1000`  
    \`입력받을 기둥 혹은 보의 정보의 데이터 개수 == 4'

2.  바닥에 보를 설치하는 경우는 없다.  
    벽면을 벗어나게 설치하는 경우는 없다.  
    구조물은 교차점 좌표를 기준으로 보는 오른쪽, 기둥은 위쪽 방향으로 설치 또는 삭제한다.  
    구조물이 겹치거나, 없는 것을 삭제하는 경우는 없습니다.

3.  **구현&시뮬레이션** 문제

4.  반환하는 데이터는 `x`, `y`, `기둥` 순으로 정렬하여 반환한다.

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
n = 5
build_frame = [[1,0,0,1],[1,1,1,1],[2,1,0,1],[2,2,1,1],[5,0,0,1],[5,1,0,1],[4,2,1,1],[3,2,1,1]]
```

#### 실행결과

```python
[[1,0,0],[1,1,1],[2,1,0],[2,2,1],[3,2,1],[4,2,1],[5,0,0],[5,1,0]]
```

<br>

### ⌨️ 문제 풀이

1.  `build_frame`을 순회하면서, 각 `frame`에서 `x`, `y`, `a`, `b` 를 구별하여 시뮬레이션을 합니다.  
    **a 는 기둥과 보의 구별, b는 삽입, 삭제의 구별에 사용합니다.**
2.  만약 `b`가 삽입에 해당할 경우, `(x, y, a)` 를 `answer`에 저장하고 `check()`함수를 호출하여  
    방금 세운 구조물이 전체적으로 가능한 구조물인지 확인합니다.
3.  `check` 함수에서 `False`를 반환한 경우, `answer`에서 `(x, y, a)`를 삭제합니다.  
    `check` 함수에서 `True`를 반환한 경우, 넘어갑니다.
4.  만약 `b`가 삭제에 해당할 경우, `(x, y, a)` 를 `answer`에서 삭제합니다.  
    `check` 함수에서 `False`를 반환한 경우, `answer`에서 `(x, y, a)`를 다시 추가합니다.  
    `check` 함수에서 `True`를 반환한 경우, 넘어갑니다.
5.  `check` 함수에서는 현재 구조물이 정상인지에 대해 판별합니다.
6.  현재 검사하는 구조물의 종류가 `보`라면 아래의 조건에 해당하지 않는 경우, `False`를 반환합니다.
7.  `if y != 0 and([x + 1, y - 1, 0] in answer or [x, y - 1, 0] in answer or ([x - 1, y, 1] in answer and [x + 1, y, 1] in answer)):`
8.  현재 검사하는 구조물의 종류가 `기둥`이라면 아래의 조건에 해당하지 않는 경우, `True`를 반환합니다.
9.  `if y == 0 or [x - 1, y, 1] in answer or [x, y, 1] in answer or [x, y - 1, 0] in answer:`

<br>

### 🖥 소스 코드

```python
def check(answer):
    for x, y, a in answer:
        if a:
            # 보
            """보는 한쪽 끝 부분이 기둥 위에 있거나, 또는 양쪽 끝 부분이 다른 보와 동시에 연결되어 있어야 합니다."""
            if y != 0 and([x + 1, y - 1, 0] in answer or [x, y - 1, 0] in answer or ([x - 1, y, 1] in answer and [x + 1, y, 1] in answer)):
                continue
            else:
                return False
        else:
            # 기둥
            """기둥은 바닥 위에 있거나 보의 한쪽 끝 부분 위에 있거나, 또는 다른 기둥 위에 있어야 합니다."""
            if y == 0 or [x - 1, y, 1] in answer or [x, y, 1] in answer or [x, y - 1, 0] in answer:
                continue
            else:
                return False
    return True


def solution(n, build_frame):
    answer = []

    for frame in build_frame:
        x, y, a, b = frame

        if b:
            # install
            answer.append([x, y, a])
            if not check(answer):
                answer.remove([x, y, a])
        else:
            # remove
            answer.remove([x, y, a])
            if not check(answer):
                answer.append([x, y, a])

    return sorted(answer)
```

<br>

## 💾 느낀점

1.  check 함수를 구현하는 것이 힘이 들었다.
2.  구현 연습은 반복만이 답이 아닌가 싶다. 더 열심히 풀어야겠다.