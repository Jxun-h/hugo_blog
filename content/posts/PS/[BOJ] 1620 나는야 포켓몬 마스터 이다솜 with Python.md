---
author: ["Jxun-h"]
title: "[BOJ] 1620 나는야 포켓몬 마스터 이다솜 with Python"
date: "2021-08-30"
description: ""
summary: ""
tags: ["자료구조", "PS", "해시맵", "알고리즘", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1620" target="_blank">BOJ 1620 나는야 포켓몬 마스터 이다솜</a>

<br>

### 💡 조건 및 풀이

1.  도감에 수록되어 있는 포켓몬의 수 `N`, 맞추어야할 문제의 개수 `M`
2.  범위는 `1 <= N, M <= 100000` 이다.
3.  **자료구조를 이용하는 문제**
4.  문자열로 입력이 들어오면 도감에 수록된 포켓몬의 번호를 출력한다.
5.  숫자로 입력이 들어오면 도감에 수록된 포켓몬의 이름을 출력한다.

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
26 5
Bulbasaur
Ivysaur
Venusaur
Charmander
Charmeleon
Charizard
Squirtle
Wartortle
Blastoise
Caterpie
Metapod
Butterfree
Weedle
Kakuna
Beedrill
Pidgey
Pidgeotto
Pidgeot
Rattata
Raticate
Spearow
Fearow
Ekans
Arbok
Pikachu
Raichu
25
Raichu
3
Pidgey
Kakuna
```

#### 실행결과

```python
Pikachu
26
Venusaur
16
14
```

<br>

### ⌨️ 문제 풀이

1.  `key - value` 로 매핑되는 자료구조를 사용한다. - `dict`
2.  이름만 저장하는 리스트를 사용한다 - `list`
3.  문자열로 입력이 들어왔을 때, `dict` 자료형에서 매핑된 번호를 꺼낸다.
4.  숫자로 입력이 들어왔을 때, `list` 자료형에서 매핑된 이름을 꺼낸다.

<br>

### 🖥 소스 코드

```python
import sys

n, m = map(int, sys.stdin.readline().split())
pokemon = {}
pokemon_nm = []

for i in range(n):
    nm = sys.stdin.readline().rstrip()
    pokemon[nm] = i
    pokemon_nm.append(nm)

for _ in range(m):
    c = sys.stdin.readline().rstrip()
    if c.isnumeric():
        print(pokemon_nm[int(c) - 1])
    else:
        print(pokemon[c] + 1)
```

<br>

### 💾 느낀점

-   `key - value` 로 매핑되는 dict 자료형으로 구현하기로 결정했는데,  
    문제를 보고 바로 떠올린 것에 대해서 큰 뿌듯함이 들었다.
-   문제를 쉽게 풀어서 그런지, 기분좋은 공부의 시작이 되었다.