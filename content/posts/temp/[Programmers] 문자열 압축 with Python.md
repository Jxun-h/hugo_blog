---
author: ["Jxun-h"]
title: "[Programmers] 문자열 압축 with Python"
date: "2021-09-12"
description: ""
summary: ""
tags: ["구현", "PS", "문자열", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/60057" target="_blank">Programmers - 문자열 압축</a>

<br>

## 💡 조건 및 풀이

1.  입력 받는 의 길이는 `1 <= s <= 1000`, 소문자로만 이루어져 있다.
2.  문자열을 1개 단위로 자르는 것부터 s의 길이 만큼 자르는 것까지 계산
3.  **완전탐색, 구현 문제**
4.  문자열을 자르고 숫자를 붙이는 것에서 쓸데 없는 문자가 들어가지 않도록 주의

<br>

## 🔖 예제 및 실행결과

#### 예제

```
print(solution("aabbaccc"))
print(solution("ababcdcdababcdcd"))
print(solution("abcabcdede"))
print(solution("abcabcabcabcdededededede"))
print(solution("xababcdcdababcdcd"))
```

#### 실행결과

```
7
9
8
14
17
```

<br>

## ⌨️ 문제 풀이

1.  `answer`의 값을 `s`의 길이로 초기화.  
    `s`의 길이만큼 자른것이 가장 짧을 수 있기 때문에 s의 길이로 초기화한다.
2.  `1개부터 s의 길이`만큼 잘라주면서 진행을 할 것이기 때문에 `1부터 s+1` 까지 반복문을 진행
3.  **자른 문자열은 이미 1개만큼 잘랐기 때문에 `cnt = 1` 로 초기화**
4.  자른 문자열과 같은 문자열이 진행하면서 있을 경우, `cnt += 1`
5.  자른 문자열과 다른 문자열이 발견되었을 경우, **검사할 문자를 교체**한다  
    지금까지 검사해주던 단어와 늘려온 cnt를 std에 넣어주고 다시 검사 진행.
6.  검사가 끝난 뒤, `std`의 길이가 기존의 `answer` 보다 작다면 갱신.

<br>

## 🖥 소스 코드

```python
def solution(s):
    k = len(s)
    answer = k

    for idx in range(1, k + 1):
        std = ''
        checker = s[0: idx]
        std += checker
        start, end = 0, idx

        cnt = 1

        for i in range(idx, k + 1, idx):
            if i == k:
                if cnt <= 1:
                    break
                else:
                    std += str(cnt)
                break

            if checker == s[start + i:end + i]:
                cnt += 1

            elif cnt <= 1:
                std += s[start + i:end + i]
                checker = s[start + i:end + i]
                continue

            else:
                std += str(cnt)
                cnt = 1
                std += s[start + i:end + i]
                checker = s[start + i:end + i]

        answer = min(answer, len(std))

    return answer
```

<br>

## 💾 느낀점
-   나는 구현이 매우 약하기 때문에 연습하기 굉장히 좋은 문제였던 것 같다.