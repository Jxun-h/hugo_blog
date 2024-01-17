---
author: ["Jxun-h"]
title: "[Programmers] 표 편집 with Python"
date: "2021-10-17"
description: ""
summary: ""
tags: ["연결리스트", "PS", "자료구조", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/81303" target="_blank">Programmers - 표 편집</a>

<br>

## 💡 조건 및 풀이

1.  표의 원본 행의 개수를 나타내는 변수 `n`  
    `5 ≤ n ≤ 1,000,000`
2.  처음에 선택되어 있는 행의 위치 `k`  
    `0 ≤ k < n`
3.  수행한 명령어들이 담긴 문자열 배열 `cmd`  
    `1 ≤ cmd의 원소 개수 ≤ 200,000`
4.  cmd의 각 원소는 `"U X", "D X", "C", "Z"` 중 하나
5.  **Linked List 자료구조 문제**
6.  표의 모든 행을 제거하여, 행이 하나도 남지 않는 경우는 입력으로 주어지지 않는다.
7.  원래대로 복구할 행이 없을 때(즉, 삭제된 행이 없을 때) "Z"가 명령어로 주어지는 경우는 없다.
8.  정답은 표의 0행부터 n - 1행까지에 해당되는 O, X를 순서대로 이어붙인 문자열 형태로 return

<br>

## 🔖 예제 및 실행결과

#### 예제

```python
print(solution(8, 2, ["D 2", "C", "U 3", "C", "D 4", "C", "U 2", "Z", "Z"]))
print(solution(8, 2, ["D 2", "C", "U 3", "C", "D 4", "C", "U 2", "Z", "Z", "U 1", "C"]))
```

#### 실행결과

```python
"OOOOXOOO"
"OOXOXOOO"
```

<br>

## ⌨️ 문제 풀이

1.  Double Linked List 자료구조를 알고, 구현할 수 있다면 풀이가 가능한 문제이다.
2.  Double Linked List 는 쉽게 말해 각 노드의 포인터가 다음, 혹은 이전의 노드를 가리키는 정보를 두개 담고 있다.
3.  연결리스트를 사용해 cmd 에 있는 명령을 수행하기 전의 원본 표의 데이터를 입력한다.

```python
class Node:
 def __init__(self, data=None, state=1):
     # 노드의 정보, 값을 저장
     self.value = data
     # 노드가 가지고 있을 전, 후를 가리키는 값은 None으로 초기화
     self.next = None
     self.priv = None
```

```python
def __init__(self):
    self.header = Node()
    self.tail = Node()
    self.header.next = self.tail
    self.header.priv = self.header

    self.tail.next = self.tail
    self.tail.priv = self.header
    self.pointer = self.header
```

```python
linkedlist = DoubleLinkedList()
pointer = linkedlist.header
for i in range(n):
    # 노드를 추가함
    linkedlist.add(Node(i))
```

4.  가장 처음에 가리키고 있는 포인터를 정해주어야하기 때문에 현재 연결리스트의 포인터를 k로 맞춰주는 작업을 한다.

```python
# 포인터의 값이 k와 다르면 계속 반복 
    while pointer.value != k: 
    # 포인터는 현재 포인터의 다음 것을 가리킨다. 
    pointer = pointer.next
```

5.  cmd를 순회하면서 요쳉에 대한 작업을 진행한다.  
    삭제를 진행하고, 복구를 하는 작업은 stack(list) 을 하나 만들어, 삭제가 진행됐을 때 저장한다.  
    복구를 할 때는 리스트에서 pop 을 하여 데이터를 꺼내오면 된다.
6.  삭제의 작업은 다음과 같다.  
    삭제될 노드를 미리 stack 에 넣어준 뒤,  
    현재의 포인터 기준으로 이전 노드에서 자신을 가리키던 것을 다음 노드를 가리키게 해주면 된다.
7.  ```python
    def delete(self, pointer): 
        if pointer.priv == self.header: 
            self.header.next = pointer.next 
            pointer.next.priv = self.header 
            return self.header.next 
        elif pointer.next == self.tail: 
            _pointer = pointer.priv 
            self.tail.priv = _pointer 
            _pointer.next = self.tail 
            return _pointer 
        else: 
            _pointer = pointer.next 
            pointer.priv.next = pointer.next 
            pointer.next.priv = pointer.priv 
            return _pointer
    ```
8.  복구의 작업은 다음과 같다.  
    복구될 노드를 stack에서 뽑아 변수에 저장한 뒤, 추가를 해준다.
9.  ```python
    def add(self, node): 
        self.pointer.next = node 
        node.priv = self.pointer 
        node.next = self.tail 
        self.pointer = node
    ```
10.  가리키는 곳을 이동하는 것은 이동하려는 칸의 수만큼 반복문을 통해 옮겨주면 된다.
11. ```python
    def move(self, pointer, v, step): 
        for _ in range(step): 
            if v == 'D': 
                pointer = pointer.next 
            else: 
                pointer = pointer.priv 
        return pointer
    ```

<br>


## 🖥 소스 코드

```python
class Node:
    def __init__(self, data=None, state=1):
        # 노드의 정보, 값을 저장
        self.value = data
        # 노드가 가지고 있을 전, 후를 가리키는 값은 None으로 초기화
        self.next = None
        self.priv = None


class DoubleLinkedList:
    def __init__(self):
        self.header = Node()
        self.tail = Node()
        self.header.next = self.tail
        self.header.priv = self.header

        self.tail.next = self.tail
        self.tail.priv = self.header
        self.pointer = self.header

    def add(self, node):
        self.pointer.next = node
        node.priv = self.pointer
        node.next = self.tail
        self.pointer = node

    def move(self, pointer, v, step):
        for _ in range(step):
            if v == 'D':
                pointer = pointer.next
            else:
                pointer = pointer.priv
        return pointer

    def delete(self, pointer):
        if pointer.priv == self.header:
            self.header.next = pointer.next
            pointer.next.priv = self.header
            return self.header.next

        elif pointer.next == self.tail:
            _pointer = pointer.priv
            self.tail.priv = _pointer
            _pointer.next = self.tail
            return _pointer

        else:
            _pointer = pointer.next
            pointer.priv.next = pointer.next
            pointer.next.priv = pointer.priv
            return _pointer

    def insert(self, pointer):
        pointer.priv.next = pointer
        pointer.next.priv = pointer


def get_answer(n, linkedlist):
    # 답이 될 리스트 생성
    answer = ['X' for _ in range(n)]

    # 연결리스트의 첫 헤더부터 포인터를 따라 순차적으로 방문하여
    # answer 원소 갱신
    pointer = linkedlist.header.next
    while pointer != linkedlist.tail:
        answer[pointer.value] = 'O'
        pointer = pointer.next

    return ''.join(answer)


def solution(n, k, cmd):
    # double linked list 초기화
    linkedlist = DoubleLinkedList()
    # 포인터 설정
    pointer = linkedlist.header
    # 삭제 요청 수행 시 삭제된 노드를 넣을 쓰레기통
    stack = []

    for i in range(n):
        # 노드를 추가함
        linkedlist.add(Node(i))

    # 포인터의 값이 k와 다르면 계속 반복
    while pointer.value != k:
        # 포인터는 현재 포인터의 다음 것을 가리킨다.
        pointer = pointer.next

    # 요청 문자에 대하 수행 시작
    for string in cmd:
        # 삭제 요청
        if string == 'C':
            # 현재 삭제될 포인터를 쓰레기통에 넣음
            stack.append(pointer)
            # 연결 리스트에서 노드를 삭제
            pointer = linkedlist.delete(pointer)

        # 복구 요청
        elif string == 'Z':
            # 쓰레기 통에 가장 마지막으로 추가된 노드 추출
            # == 연결 리스트에서 가장 최근에 삭제된 노드
            _pointer = stack.pop()
            # 연결리스트에 삽입
            linkedlist.insert(_pointer)

        else:
            v, step = string.split()
            # 포인터 이동
            pointer = linkedlist.move(pointer, v, int(step))

    # 답 만들기
    answer = get_answer(n, linkedlist)
    return answer


print(solution(8, 2, ["D 2", "C", "U 3", "C", "D 4", "C", "U 2", "Z", "Z"]))
print(solution(8, 2, ["D 2", "C", "U 3", "C", "D 4", "C", "U 2", "Z", "Z", "U 1", "C"]))
```

<br>

## 💾 느낀점

-   문제를 풀지 못해서 다른 분의 아이디어를 참고하여 연결리스트를 먼저 구현해보고자 했었다.  
    자료구조를 class 형식으로 구현하는 연결리스트에 놀랬다.  
    처음보는 자료구조였고, 감탄할 수밖에 없는 풀이였다.  
    그 후 이중 연결 리스트를 보면서 비슷한 유형의 문제가 나온다면  
    연결리스트를 구현해서 풀어보고 싶다는 생각을 했다.
-   단순히 stack에 삭제한 노드 번호를 넣고, 노드번호를 이분탐색으로 제자리에 복구하려는 시도를 했으나  
    구현부분이 까다롭고 구현하면서도 조금씩 제한되고 구현하기에 어려운 부분이 있어 풀이를 참고 했다.
-   현재까지 2회 풀었는데, 아직 이전 소스를 참고하지 않고 완벽하게 이중 연결 리스트를 구현하기가 어려웠다.  
    매일 볼때마다 조금은 새로운 이중 연결 리스트 구현 방법의 숙달과 관련 문제 풀이가 필요할 것 같다.