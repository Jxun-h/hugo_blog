---
author: ["Jxun-h"]
title: "[BOJ] 4779 칸토어 집합 with Python"
date: "2021-08-31"
description: ""
summary: ""
tags: ["분할정복", "PS", "재귀", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/4779" target="_blank">BOJ 4779 칸토어 집합</a>

<br>

### 💡 조건 및 풀이

1.  칸토어 집합은 0과 1 사이의 실수로 이루어진 집합.  
    구간 `[0, 1]`에서 시작해서 **각 구간을 3등분하여 가운데 구간을 반복적으로 제외하는 방식**으로 만든다.
2.  `-`가 `3N`개 있는 문열에서 시작 == - 의 개수는 `3 ** N` 개
3.  **분할 정복 + 재귀 유형의 문제**
4.  `0 <= N <= 12`
5.  **파일의 끝에서 입력을 멈춘다**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
0
1
3
2
```

#### 실행결과

```python
-
- -
- -   - -         - -   - -
- -   - -
```

<br>

### ⌨️ 문제 풀이

1.  칸토어 집합은 **각 구간을 3등분**, **반복적으로 가운데 구간을 제외하는 방식**
2.  **파일의 끝에서 입력을 멈춘다** 라는 말은 무한루프를 돌다가,  
    입력받은 `N`이 비어있는 문자열 `''`이면 `break`
3.  입력받은 `N`이 0, `-`의 개수가 1이라면 `print('-')`
4.  `(N ** 3) * '-' == 하이픈의 개수`
5.  만들어진 하이픈을 분할 정복 함수에 넣는다.  
    각 파라미터는 `3 ** N`개의 하이픈과 인덱스 번호이다.
6.  인덱스 번호는 세등분이 된 문자열의 각 인덱스 번호이며, **재귀를 통해 인덱스 번호가 1인  
    문자열을 공백으로 만들어주면 된다.**
7.  **문자열은 파라미터로 받은 문자열 길이를 3으로 나누어**  
    그 길이만큼 리스트를 슬라이싱해 arr 리스트에 넣는다.
8.  반환 조건은 아래의 두가지로 만들었다.
    -   문자열의 길이가 3이고 인덱스 번호가 1이 아닐 때에는 '- -'을 리턴
    -   문자열의 길이가 3보다 같거나 크며, 인덱스 번호가 1일 때는 문자열의 길이만큼 공백을 반환

<br>

### 🖥 소스 코드

```python
from sys import stdin, setrecursionlimit
setrecursionlimit(10 ** 6)


def div(s, idx):
    ls = len(s)
    if ls == 3 and idx != 1:
        return '- -'
    elif ls >= 3 and idx == 1:
        return s.replace('-', ' ')

    arr = []

    for i in range(0, ls, ls // 3):
        arr.append(string[i:i+ls//3])

    k = div(arr[0], 0) + div(arr[1], 1) + div(arr[2], 2)
    return k


while 1:
    k = '-'
    n = stdin.readline().rstrip()
    if n == '':
        break
    num = (3 ** int(n))
    if num == 1:
        print('-')
        continue

    string = k * num
    arr = div(string, 0)
    print(arr)
```

<br>

### 💾 느낀점

-   분할 정복을 사용하기로 하고 인덱스를 같이 파라미터 값으로 넣자고 생각했다.  
    좋은 아이디어가 한번에 떠올라서 매우 좋았다.
-   성공적인 풀이였다. 재귀 사용 실력이 최악이라 사용자체가 많이 힘들었지만  
    예전보다는 사용하기 매우 수월해졌다.