---
author: ["Jxun-h"]
title: "[BOJ] 1043 거짓말 with Python"
date: "2021-10-20"
description: ""
summary: ""
tags: ["자료구조", "PS", "그래프이론", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1043" target="_blank">BOJ 1043 거짓말</a>

<br>

### 💡 조건

1.  `N, M`은 `50 이하의 자연수` 각각 사람의 수, 파티의 수  
    진실을 아는 사람의 수는 `0 이상 50 이하의 정수`  
    각 파티마다 오는 사람의 수는 `1 이상 50 이하의 정수`
2.  지민이는 **모든 파티에 참가**해야한다.  
    지민이는 이야기를 과장되게 한다. 또한 지민이는 거짓말쟁이가 되기 싫다.  
    **이야기의 진실을 아는 사람이 파티에 있으면 과장해서 말할 수 없다.**
3.  과장된 이야기를 할 수 있는 파티 개수의 `최댓값`을 구하는 문제.
4.  **자료구조의 활용을 요구하는 유형의 문제**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
4 5
1 1
1 1
1 2
1 3
1 4
2 4 1
```

#### 실행결과

```python
2
```

<br>

### ⌨️ 문제 풀이

1.  `cnt`라는 리스트에 파티의 수만큼 원소를 만들어주고, 각 값을 `1`로 둔다.  
    이는 **파티에서 과장되게 말을 할 수 있다는 가정하에 `1`로 둔 것.**  
    또한 각 파티의 구성원을 `party` 리스트에 각각 집어넣어준다.
2.  파티의 수만큼 다시 순회하면서 각 `party`의 번호와 구성원을 뽑아 반복문을 돌리기 위해 `enumerate` 를 사용해준다.  
    **enumerate 함수는 리스트를 순회하면서 리스트의 각 원소의 인덱스와 원소를 반환한다.**
3.  파티의 구성원과 진실을 아는 사람들간에 **교집합이 존재**한다면, `cnt` 리스트의 해당 번호에 해당하는 값을 `0`으로 변경한다.  
    **그 파티는 진실만을 말할 수 있는 파티라는 것**이다.  
    그 후, 파티원을 진실을 알고 있는 사람들이 저장되어 있는 `set()` 자료형에 `update` 시켜준다.  
    `update` 와 `|=` 이 둘은 같은 효과를 볼 수 있다.
4.  `cnt` 리스트의 합을 구해 출력한다.

<br>

### 🖥 소스 코드

```python
from sys import stdin

n, m = map(int, stdin.readline().split())
trues = set(list(map(int, stdin.readline().split()))[1:])
party = []
cnt = []

for _ in range(m):
    data = set(map(int, stdin.readline().split()[1:]))
    if data:
        party.append(data)
        cnt.append(1)

for _ in range(m):
    for i, p in enumerate(party):
        if trues & p:
            cnt[i] = 0
            trues |= p

print(sum(cnt))
```

<br>

### 💾 느낀점

1.  `set` 집합자료형의 강력함을 알 수 있는 문제였다.
2.  문제를 잘 읽고 자료구조를 활용하면 풀 수 있는 문제였다.
3.  이 문제를 한번에 풀지 못했다. 아직 활용이 부족한 것 같다.