---
author: ["Jxun-h"]
title: "[BOJ] 10384 팬그램 with Python"
date: "2022-03-03"
description: ""
summary: ""
tags: ["자료구조", "PS", "구현", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/10384" target="_blank">BOJ 10384 팬그램</a>

<br>

### 💡 조건

1.  팬그램은 모든 알파벳을 적어도 한 번씩을 사용한 영어 문장을 말한다.
2.  더블 팬그램은 모든 알파벳을 적어도 두 번씩은 사용한 문장을 말하고, 트리플 팬그램은 모든 알파벳을 적어도 세 번씩은 사용한 문장을 말한다.
3.  입력은 여러 줄의 테스트케이스들로 이루어진다.  
    첫째 줄에 테스트케이스의 수 n이 주어진다.  
    각 테스트케이스는 영어 소문자와 대문자, 특수기호들로 이루어진다.
4.  팬그램이 아닐 경우 - Not a pangram  
    팬그램일 경우 - Pangram!  
    더블 팬그램일 경우 - Double pangram!!  
    트리플 팬그램일 경우 - Triple pangram!!!
5.  **구현** 유형의 문제

<br>

### 🔖 예제 및 실행결과

#### 예제

```py
3
The quick brown fox jumps over a lazy dog.
The quick brown fox jumps over a laconic dog.
abcdefghijklmNOPQRSTUVWXYZ-zyxwvutsrqpon   2013/2014      MLKJIHGFEDCBA
```

#### 실행결과

```py
Case 1: Pangram!
Case 2: Not a pangram
Case 3: Double pangram!!
```

<br>

### ⌨️ 문제 풀이

1.  테스트케이스만큼 반복문을 진행하면서, 결과값을 저장할 res 변수를 'Not a pangram'으로 초기화한다.
2.  string에 어떤 검사할 문자열을 입력받고, 알파벳을 몇번 썼는지 검사할 alphabet 이라는 2차원 배열을 만든다.
3.  string을 순회하면서 알파벳이 아닐 경우 continue, 알파벳일 경우 해당 알파벳을 True로 체크해주면된다.
4.  최대 트리플 팬그램까지 밖에 없으니 idx 를 0부터 시작하여 2까지 늘려주고, 다시 0으로 만들어주는 작업을 통해서 알파벳이 사용되었는지 체크한다.
5.  alphabet 리스트를 순회하면서 리스트에 False가 없다면 cnt + 1, 있다면 break를 한다.
6.  cnt에 따라 결과값 res를 갱신하고 출력양식에 맞게 출력한다.

<br>

### 🖥 소스 코드

```py
from sys import stdin

for i in range(1, int(stdin.readline()) + 1):
    res = 'Not a pangram'
    string = stdin.readline().rstrip()

    alphabet = [[False] * 26 for _ in range(3)]

    for j in string:
        idx = 0
        if not j.isalpha():
            continue
        else:
            while 1:
                if not alphabet[idx][ord(j.lower()) - 97]:
                    alphabet[idx][ord(j.lower()) - 97] = True
                    break
                else:
                    idx += 1

                if idx > 2:
                    idx = 0
                    break

    cnt = 0
    for data in alphabet:
        if False in data:
            break
        else:
            cnt += 1

    if cnt == 1:
        res = 'Pangram!'
    elif cnt == 2:
        res = 'Double pangram!!'
    elif cnt == 3:
        res = 'Triple pangram!!!'

    print('Case {}: {}'.format(i, res))
```

<br>

### 💾 느낀점

1.  dict로도 풀수 있지 않을까? 라는 생각이 든다.