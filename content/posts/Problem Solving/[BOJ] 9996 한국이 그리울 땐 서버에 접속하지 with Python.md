---
author: ["Jxun-h"]
title: "[BOJ] 9996 한국이 그리울 땐 서버에 접속하지 with Python"
date: "2022-06-29"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "문자열", "브루트포스", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/9996" target="_blank">BOJ 9996 한국이 그리울 땐 서버에 접속하지</a>

<br>

### 💡 조건

1.  선영이는 한국에 두고온 서버에 접속해서 디렉토리 안에 들어있는 파일 이름을 보면서 그리움을 잊기로 했다.  
    매일 밤, 파일 이름을 보면서 파일 하나하나에 얽힌 사연을 기억하면서 한국을 생각하고 있었다.  
    한국에 있는 서버가 망가졌고, 그 결과 특정 패턴과 일치하는 파일 이름을 적절히 출력하지 못하는 버그가 생겼다.

2.  패턴은 알파벳 소문자 여러 개와 별표(*) 하나로 이루어진 문자열이다.  
    파일 이름이 패턴에 일치하려면, 패턴에 있는 별표를 알파벳 소문자로 이루어진 임의의 문자열로 변환해 파일 이름과 같게 만들 수 있어야 한다.

3.  별표는 빈 문자열로 바꿀 수도 있다.  
    예를 들어, "abcd", "ad", "anestonestod"는 모두 패턴 "a*d"와 일치한다. 하지만, "bcd"는 일치하지 않는다.

4.  패턴과 파일 이름이 모두 주어졌을 때, 각각의 파일 이름이 패턴과 일치하는지 아닌지를 구하는 문제

5.  첫째 줄에 파일의 개수 N이 주어진다. (1 ≤ N ≤ 100)  
    문자열의 길이는 100을 넘지 않으며, 별표는 문자열의 시작과 끝에 있지 않다.  
    다음 N개 줄에는 파일 이름이 주어진다.

6.  총 N개의 줄에 걸쳐서, 입력으로 주어진 i번째 파일 이름이 패턴과 일치하면 "DA", 일치하지 않으면 "NE"를 출력한다.

7.  **구현, 문자열, 브루트포스** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
6
h*n
huhovdjestvarnomozedocisvastan
honijezakon
atila
je
bio
hun
```

#### 실행결과

```py
DA
DA
NE
NE
NE
DA
```

<br>

### ⌨️ 문제 풀이

1.  문제에서 보면 패턴은 알파벳 소문자와 별표 한 개로 이루어져있다는 정보가 있다.  
    패턴은 *를 기준으로해서 split 해주고, 패턴 시작과 패턴 끝으로 구분한다.

2.  나눈 패턴의 시작과 끝을 비교하여 아래에 해당되는지 확인한다.
    1.  1.입력받은 문자열을 시작 패턴의 길이만큼 잘라서 시작 패턴과 같은지 확인한다.
    2.  2.입력받은 문자열을 끝 패턴까지 잘라서 나눈 끝 패턴과 같은지 확인한다.
    3.  3.패턴을 의미하는 *을 제외한 문자열의 길이가 입력 받은 문자열의 길이보다 작거나 같은지 확인한다.

3.  위 세가지 조건에 해당되지 않는 경우, match_tf 함수에서 False 를 return 한다.

4.  match_tf 가 False 일 경우, 'DA' 출력  
    match_tf 가 Ture 일 경우, 'NE' 출력

<br>

### 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
pattern = stdin.readline().rstrip()


def match_tf(p, s):
    p = p.split('*')
    start_m, end_m = p[0], p[1]
    if s[:len(start_m)] == start_m and s[-len(end_m):] == end_m and len(''.join(p)) <= len(s):
        return True
    return False


for _ in range(n):
    string = stdin.readline().rstrip()
    if match_tf(pattern, string):
        print('DA')
    else:
        print('NE')
```
