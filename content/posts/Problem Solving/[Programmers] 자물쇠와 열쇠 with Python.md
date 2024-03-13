---
author: ["Jxun-h"]
title: "[Programmers] 자물쇠와 열쇠 with Python"
date: "2021-11-29"
description: ""
summary: ""
tags: ["구현", "PS", "시뮬레이션", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["Programmers"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/60059" target="_blank">Programmers 자물쇠와 열쇠 with Python</a>

<br>

### 💡 조건

1.  `key`는 `M x M(3 ≤ M ≤ 20, M은 자연수)` 크기 2차원 배열  
    `lock`은 `N x N(3 ≤ N ≤ 20, N은 자연수)` 크기 2차원 배열  
    `M은 항상 N 이하`, `key`와 `lock`의 원소는 `0 또는 1`
2.  자물쇠는 홈이 있으며, 열쇠도 돌기가 있다. 열쇠는 회전이 가능하다.
3.  자물쇠 부분이 회전할 수 있는 열쇠와 겹쳐져서 모두 1이 된다면 열 수 있으니 `True`, 열 수 없다면 `False`를 반환
4.  **구현 & 시뮬레이션 유형의 문제**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
print(solution([[0, 0, 0], [1, 0, 0], [0, 1, 1]], [[0, 0, 0, 0], [1, 1, 1, 0], [0, 0, 0, 0], [1, 0, 1, 0]]))
```

#### 실행결과

```python
true
```

<br>

### ⌨️ 문제 풀이

1.  `N`과 `M`의 최대 크기가 `20`이니, 열쇠의 최소크기인 3만큼 자물쇠의 길이에 곱해서 맵을 뻥튀기 시킨다.  
    이 작업은 열쇠를 움직이기 편하기 위해서 전체 맵의 크기를 키우는 것.
2.  맵의 크기를 세배로 넓혔다면, 원래 자물쇠를 가운데 위치에 위치시킨다.
    ```python
    for i in range(lock_l):
        for j in range(lock_l):
            new_lock[i + lock_l][j + lock_l] = lock[i][j]
    ```

3.  **열쇠는 총 4방향으로 돌 수 있으니**, 열쇠를 미리 한 번 돌리고 이동시키면서 자물쇠가 열리는지 체크하면 된다.
    ```python
    key = turn_key(key_l, key)

    def turn_key(l, key):  
        new_key = [item[:] for item in key]
        for i in range(l):
            for j in range(l):
                new_key[i][j] = key[l - (j + 1)][i]

    return new_key
    ```

<br>

4.  열쇠를 0, 0 부터 new_lock 의 크기에서 key의 길이만큼 뺀 값까지 이동시키면서 반복순회를 한다.
    ```python
    def check(lock, lock_l):  
     for i in range(lock_l):  
         for j in range(lock_l):  
             if lock[i + lock_l][j + lock_l] != 1:  
                 return False  
     return True
    ```

<br>

### 🖥 소스 코드

```python
def turn_key(l, key):
    new_key = [item[:] for item in key]

    for i in range(l):
        for j in range(l):
            new_key[i][j] = key[l - (j + 1)][i]

    return new_key


def check(lock, lock_l):
    for i in range(lock_l):
        for j in range(lock_l):
            if lock[i + lock_l][j + lock_l] != 1:
                return False
    return True


def solution(key, lock):
    key_l = len(key)
    lock_l = len(lock)
    new_lock = [[0] * (lock_l * 3) for _ in range(lock_l * 3)]

    new_len = len(new_lock)

    for i in range(lock_l):
        for j in range(lock_l):
            new_lock[i + lock_l][j + lock_l] = lock[i][j]

    for i in range(4):
        key = turn_key(key_l, key)

        for i in range(new_len - key_l):
            for j in range(new_len - key_l):

                for k in range(key_l):
                    for p in range(key_l):
                        new_lock[i + k][j + p] += key[k][p]

                if check(new_lock, lock_l):
                    return True

                else:
                    for k in range(key_l):
                        for p in range(key_l):
                            new_lock[i + k][j + p] -= key[k][p]

    return False
```

<br>

### 💾 느낀점

1.  열쇠를 돌리는 것에서 헤맬뻔했지만, 반복 숙달덕에 잘 할 수 있었다.
2.  자물쇠의 전체 크기를 키워서 하는 방법은 N, M 의 크기가 작은 것을 확인하고 생각해낼 수 있었다.
3.  역시 시뮬레이션 & 구현 문제는 어렵다.