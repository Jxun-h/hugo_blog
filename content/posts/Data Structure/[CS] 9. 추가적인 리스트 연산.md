---
author: ["Jxun-h"]
title: "[CS] 9. 추가적인 리스트 연산"
date: "2022-07-12 13:31:00"
description: ""
summary: ""
tags: ["자료구조", "CS", "Computer Science"]
categories: ["Computer Science"]
series: ["Computer Science"]
ShowToc: false
---

<br>

## 📌 추가적인 리스트 연산

<br>

### 💡 추가적인 리스트 연산들

1.  단일 연결 리스트(Chain) 에 대한 연산
    1.  체인의 방향을 반대로 : invert()
    2.  두 개의 체인을 통합 : concatenate()

2.  원형 리스트에 대한 연산
    1.  원형 연결리스트의 길이를 계산하는 연산 : length()
    2.  원형 연결리스트의 제일 앞에 새로운 노드 삽입 : insert\_front()

<br>

### 💡 Invert 함수

1.  포인터 3개를 사용해 가리키는 포인터를 변경해준다.
2.  lead, middle, tail 세 개의 포인터를 사용한다고 하면, return 값은 middle 이다.

<br>

### 💡 concatenate 함수

1.  A 체인 혹은 B 체인이 NULL 일 경우, 나머지를 반환한다.
2.  A를 순회하면서 접근하고, A 마지막 노드의 포인터를 B로 가리켜준다.

<br>

### 💡 원형 연결리스트의 순회

1.  처음 데이터는 별도로 처리해주고, 무한루프를 방지할 수 있게 코드를 작성한다.

```c++
# 체인 연결리스트의 순회
struct node *ptr;
for (ptr A -> link; ptr != null; ptr = ptr -> link)
    sum += ptr -> data;
```

```c++
# 원형 연결리스트의 순회
struct node *ptr = A;
sum += ptr -> data;
for (ptr A -> link; ptr != A; ptr = ptr -> link)
    sum += ptr -> data;
```

<br>

### 💡 원형 연결리스트의 이름

1.  첫번째 Node 를 Pointing
2.  마지막 Node 를 pointing
    1.  마지막 노드를 가리킬 경우, 다음 연산의 복잡성은 O(1)
        1.  리스트의 첫번째 위치에 노드 추가/삭제
        2.  리스트의 마지막 위치에 노드 추가