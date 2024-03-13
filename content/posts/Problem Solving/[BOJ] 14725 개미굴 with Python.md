---
author: ["Jxun-h"]
title: "[BOJ] 14725 개미굴 with Python"
date: "2021-11-21"
description: ""
summary: ""
tags: ["자료구조", "PS", "트라이", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/14725" target="_blank">BOJ 14725 개미굴</a>

<br>

### 💡 조건

1.  첫 번째 줄은 로봇 개미가 각 층을 따라 내려오면서 알게 된 먹이의 정보 개수 N >> `(1 ≤ N ≤ 1000)`  
    두 번째 줄부터 N+1 번째 줄까지, 각 줄의 시작은 로봇 개미 한마리가 보내준 먹이 정보 개수 K >> `(1 ≤ K ≤ 15)`  
    다음 K개의 입력은 로봇 개미가 왼쪽부터 순서대로 각 층마다 지나온 방에 있는 먹이 정보이며 먹이 이름 길이 t >> `(1 ≤ t ≤ 15)`
2.  **트라이(Trie) 자료구조**를 사용하는 문제.

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
4
2 KIWI BANANA
2 KIWI APPLE
2 APPLE APPLE
3 APPLE BANANA KIWI
```

#### 실행결과

```python
APPLE
--APPLE
--BANANA
----KIWI
KIWI
--APPLE
--BANANA
```

### ⌨️ 문제 풀이

1.  trie 클래스를 생성하고, 로봇 개미가 보내준 데이터를 `Trie` 에 담는다.

2.  클래스 내 `insert` 함수에서 데이터를 차례대로 넣는다.  
    `cur_node` 변수를 `root`로 주고, 데이터가 존재한다면 `cur_node`를 갱신,  
    데이터가 존재 하지 않는다면, 추가해준다.  
    입력 작업 반복문이 끝이 났다면, 노드의 마지막을 `'*'` 로 저장해준다.

3.  마지막 라인에서 클래스 내 출력 함수인, `print_trie` 를 `0` 을 넣어 실행해준다.  
    `l` 이 `0`이라면, `cur_node` 를 `root`로 설정해준다.  
    `cur_node`의 키 값을 정렬한 뒤, 반복문을 통해 출력해준다  
    여기서 노드의 키 값이 `'*'` 이라면 출력을 하지 않고, `print_trie` 함수를 재귀 호출해준다.  
    이때, `l`의 값은 + 1, `cur_node`는 c노드를 기준으로 넣어준다.

4.  만약 `cur_node` 의 키 값이 `'*'` 이 아니라면 `'--'` 문자열을 `l` 만큼 출력한 뒤, 노드를 출력한다

<br>

### 🖥 소스 코드

```python
from sys import stdin
n = int(stdin.readline())


class Trie:
    def __init__(self):
        self.root = {}

    def insert(self, s):
        cur_node = self.root
        for c in s:
            if c not in cur_node:
                cur_node[c] = {}
            cur_node = cur_node[c]
        cur_node['*'] = {}

    def print_trie(self, l, cur_node=None):
        if l == 0:
            cur_node = self.root

        for c in sorted(cur_node.keys()):
            if c != '*':
                print('--' * l, c, sep="")
            self.print_trie(l + 1, cur_node[c])


trie = Trie()
for _ in range(n):
    data = list(stdin.readline().split())
    trie.insert(data[1:])

trie.print_trie(0)
```

<br>

### 💾 느낀점

1.  Trie 자료구조를 공부해야 풀 수 있는 문제였다.
2.  처음보는 자료구조이기에 이해하는데에도 시간이 걸렸고, 부족한 점을 알게 되었다.
3.  로직을 보면서 공부해야할 것을 다시 한번 정리하고 공부해야겠다.