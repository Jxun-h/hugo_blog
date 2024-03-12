---
author: ["Jxun-h"]
title: "[BOJ] 2697 다음수 구하기 with Python"
date: "2022-03-01"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "문자열", "그리디", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/2697" target="_blank">BOJ 2697 다음수 구하기</a>

<br>

### 💡 조건

1.  A의 다음수는 A와 구성이 같으면서, A보다 큰 수 중에서 가장 작은 수.
2.  A와 B의 구성이 같다는 말은 A를 이루고 있는 각 자리수의 등장 횟수가, B를 이루는 각 자리수의 등장 횟수와 같을 때.
3.  첫째 줄에 테스트 케이스의 개수 T(1<=T<=1,000)가 주어진다.  
    둘째 줄부터 T개 줄에는 각 테스트 케이스가 주어진다.
4.  테스트 케이스는 한 줄로 이루어져 있으며, 수 A이다. A는 최대 80자리 자연수이다.
5.  어떤 수 A가 주어졌을 때, A의 다음수를 구하는 프로그램을 작성하는 문제.  
    만약, A의 다음수가 없을 때는 BIGGEST를 출력한다.
6.  **구현, 문자열, 그리디 알고리즘** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3
123
279134399742
987
```

#### 실행결과

```py
132
279134423799
BIGGEST
```

<br>

### ⌨️ 문제 풀이

1.  입력받은 숫자를 역순으로 탐색합니다.
2.  왼쪽에 있는 값이 오른쪽보다 작아질 경우, idx에 해당 인덱스 값을 넣어줍니다.
3.  숫자를 a 와 b 로 나누는데, 그 기준은 idx 값으로 나눌 수 있습니다.
4.  나누어진 두 숫자 중 하나라도 비어있다면, BIGGEST 를 출력합니다.
5.  (4)번의 경우가 아니라면, b 를 오름차순으로 정렬하고, b의 길이만큼 순회합니다.
6.  원래 입력 받았던 숫자의 idx 번째 숫자보다 b를 순회하는 중 i번째 숫자가 크다면,  
    i번째 숫자를 뽑아서 a에 붙이고, 나머지 b를 그대로 이어붙여줍니다.
7.  a를 문자열로 출력합니다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

for _ in range(int(stdin.readline())):
    data = list(map(int, list(stdin.readline().rstrip())))
    length, idx = len(data), 0
    for i in range(length - 1, 0, -1):
        if data[i] > data[i - 1]:
            if i == length - 1:
                idx = length - 2
            else:
                idx = i - 1
            break

    a = data[:idx]
    b = data[idx:]

    if not a or not b:
        print('BIGGEST')
    else:
        b.sort()
        for i in range(len(b)):
            if b[i] > data[idx]:
                a.append(b.pop(i))
                a.extend(b)
                break

        print(''.join(map(str, a)))
```

<br>

### 💾 느낀점

1.  문제를 한참보고도 헤맸던 문제였다.
2.  원래 이런 규칙이 있는 것처럼 모두 풀이를 써놔서 일단 풀이를 외웠던 것으로 기억했다.
3.  글을 쓰면서 다시 한번 풀이를 상기해보려고 했으나, 어려웠던 문제 중 하나인 것 같다.
4.  이러한 문제를 만나면 천천히 풀이를 생각해보자.