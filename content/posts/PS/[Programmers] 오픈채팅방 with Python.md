---
author: ["Jxun-h"]
title: "[Programmers] 오픈채팅방 with Python"
date: "2021-11-21"
description: ""
summary: ""
tags: ["자료구조", "PS", "해시맵", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["Programmers"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/42888" target="_blank">Programmers 오픈채팅방 with Python</a>

<br>

### 💡 조건

1.  채팅방에 들어오고 나가거나, 닉네임을 변경한 기록이 담긴 문자열 배열 `record`  
    모든 기록이 처리된 후, 최종적으로 방을 개설한 사람이 보게 되는 메시지를 문자열 배열 형태로 `return`
2.  `record`는 다음과 같은 문자열이 담긴 배열이며, 길이는 `1 이상 100,000 이하`
3.  모든 유저는 유저 아이디로 구분한다.  
    유저 아이디 사용자가 닉네임으로 채팅방에 입장 - `"Enter 유저 아이디 닉네임" (ex. "Enter uid1234 Muzi")`
4.  **구현 유형의 문제**

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
record = ["Enter uid1234 Muzi", "Enter uid4567 Prodo","Leave uid1234","Enter uid1234 Prodo","Change uid4567 Ryan"]
```

#### 실행결과

```python
["Prodo님이 들어왔습니다.", "Ryan님이 들어왔습니다.", "Prodo님이 나갔습니다.", "Prodo님이 들어왔습니다."]
```

<br>

### ⌨️ 문제 풀이

1.  문제의 정답을 출력할 배열 `answer`, `(상태, uid)` 정보를 저장할 배열 `result`,  
    입장과 퇴장의 문구가 담긴 배열 `status`, `(uid, 닉네임)`이 담겨있는 딕셔너리 `id_code` 를 생성한다.

2.  `record`를 순회하면서 가장 첫 정보가 `Enter` 일 경우, `id_code` 딕셔너리에 `uid: 닉네임` 형식으로 데이터를 저장한다.  
    `result`에 `(상태코드, uid)` 를 저장한다.
3.  첫 정보가 `Leave` 일 경우, `result`에 `(상태코드, uid)` 를 저장한다.

4.  첫 정보가 `Change` 일 경우, `id_code`의 `uid` 에 해당하는 닉네임을 변경한다.

5.  `result` 배열을 순회하면서 `id_code` 딕셔너리의 `uid`에 해당하는 닉네임과 스테이터스 번호를 함께 `answer` 배열에 저장한다.

6.  `answer`를 반환한다.

<br>

### 🖥 소스 코드

```python
def solution(record):
    result = []
    answer = []
    status = ["님이 들어왔습니다.", "님이 나갔습니다."]
    id_code = {}

    for r in record:
        l = r.split()

        if l[0] == 'Enter':
            id_code[l[1]] = l[2]
            result.append([0, l[1]])

        elif l[0] == 'Leave':
            result.append([1, l[1]])

        else:
            id_code[l[1]] = l[2]

    for s, uid in result:
        answer.append(id_code[uid] + status[s])

    return answer
```

<br>

## 💾 느낀점

1.  uid 번호에 따른 상태와, 닉네임을 변경하여 그에 맞게 출력하는 **구현문제**였다.
2.  상태를 저장을 어떻게 할지에 대해서 고민을 하다가 오래걸렸었는데, 직접 구현을 하고 보니 짧고 간단한 문제였다.
3.  구현 연습을 더 열심히 해야하겠다.