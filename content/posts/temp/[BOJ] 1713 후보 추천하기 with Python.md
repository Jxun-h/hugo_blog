---
author: ["Jxun-h"]
title: "[BOJ] 1713 후보 추천하기 with Python"
date: "2021-10-18"
description: ""
summary: ""
tags: ["구현", "PS", "시뮬레이션", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1713" target="_blank">BOJ 1713 후보 추천하기</a>

<br>

### 💡 조건

1.  사진틀의 개수 N이 주어진다. `(1 ≤ N ≤ 20)`  
    총 추천 횟수는 `1,000번 이하`이며 학생을 나타내는 번호는 `1부터 100까지의 자연수`
2.  사진틀의 개수와 전체 학생의 추천 결과가 추천받은 순서대로 주어졌을 때, 최종 후보가 누구인지 결정
3.  **구현 & 시뮬레이션 유형의 문제**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
3
9
2 1 4 3 5 6 2 7 2
```

#### 실행결과

```python
2 6 7
```

<br>

### ⌨️ 문제 풀이

1.  추천받은 순서대로 주어진 리스트를 순회하며 student (dict) 에 없으면 새로 추가하고,  
    student (dict) 에 있으면 + 1을 해준다.  
    만약, 새로 추가를 해야하는데 student 길이가 사진틀의 개수보다 같거나 클 경우, 가장 적게 추천 받은 학생 또는 가장 오래된 사진을 뺀다.
2.  student에 남아있는 key만 뽑아 정렬한 뒤 반환한다.

<br>

### 🖥 소스 코드

```python
from sys import stdin
import heapq


def solution(n):
    student = {}
    data = list(map(int, stdin.readline().split()))
    for s in data:
        if s not in student:
            if len(student) >= n:
                # dict를 heapq 모듈을 사용해 최솟값을 뽑아냄
                a = heapq.nsmallest(min(student), student, key=student.get)
                student.pop(a[0])

            student[s] = 1
        else:
            student[s] += 1

    return sorted(student.keys())


n = int(stdin.readline().rstrip())
r = int(stdin.readline().rstrip())
print(*solution(n))
```

### 💾 느낀점

1.  heapq 에 더 다양한 기능이 있다는 것을 검색을 통해 알았다.
2.  일반 반목 + 조건문으로 코드를 작성한 것보다 훨씬더 보기가 좋았다.