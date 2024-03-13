---
author: ["Jxun-h"]
title: "[BOJ] 1722 순열의 순서 with Python"
date: "2022-08-09 17:18:00"
description: ""
summary: ""
tags: ["자료구조", "PS", "정렬", "백준", "BOJ"]
categories: ["Algorithm"]
series: ["BOJ"]
ShowToc: false
---

<br>

## 📌 <a href="https://www.acmicpc.net/problem/1722" target="_blank">BOJ 1722 순열의 순서</a>

<br>

### 💡 조건

1.  1부터 N까지의 수를 임의로 배열한 순열은 총 N! = N×(N-1)×…×2×1 가지가 있다.

2.  임의의 순열은 정렬을 할 수 있다.  
    예를 들어 N=3인 경우 {1, 2, 3}, {1, 3, 2}, {2, 1, 3}, {2, 3, 1}, {3, 1, 2}, {3, 2, 1}의 순서로 생각할 수 있다.

3.  N이 주어지면, 아래의 두 소문제 중에 하나를 풀어야 한다.  
    k가 주어지면 k번째 순열을 구하고, 임의의 순열이 주어지면 이 순열이 몇 번째 순열인지를 출력하는 문제

4.  첫째 줄에 N(1 ≤ N ≤ 20)이 주어진다.

5.  1인 경우 k(1 ≤ k ≤ N!)를 입력받고, 2인 경우 임의의 순열을 나타내는 N개의 수를 입력받는다.  
    N개의 수에는 1부터 N까지의 정수가 한 번씩만 나타난다.

6.  **수학, 조합론** 유형의 문제

<br>

## 🔖 예제 및 실행결과

#### 예제 1

```py
4
1 3
```

#### 실행결과 1

```py
1 3 2 4
```

#### 예제 2

```py
4
2 1 3 2 4
```

#### 실행결과 2

```py
3
```

<br>

## ⌨️ 문제 풀이

1.  N이 최대 20까지라면, 브루트포스로 풀이했을 때 시간복잡도가 최악의 경우 20! = 2,432,902,008,176,640,000 가지의 경우의 수가 나온다.  
    무조건 시간초과가 날 수 밖에 없다.

2.  입력 순열이 만약 [3, 4, 1, 2]가 입력되었다고 가정해보자.  
    1로 시작하는 [1, ?, ? ,?]와 같은 순열의 경우의 개수는 3!이다.  
    2로 시작하는 [2, ?, ? ,?]와 같은 순열의 경우의 개수는 3!이다.

3.  입력을 받은 순열은 3으로 시작한다. 따라서  
    [3, 1, ?, ?]로 시작하는 순열의 경우의 개수는 2!이다.  
    [3, 2, ?, ?]로 시작하는 순열의 경우의 개수는 2!이며, 3도 마찬가지이다.

4.  이 후의 개수는 [3, 4, 1, ?] 1개.  
    2번 부터 4번의 과정을 더하면 몇 번째 순열인지 알 수가 있다.

5.  이와 같은 과정을 반대로 진행하면 K번째 순열을 출력할 수 있다.

<br>

## 🖥 소스 코드

```py
from sys import stdin

n = int(stdin.readline())
data = list(map(int, stdin.readline().split()))
cache = {}


def find_permutations(n):
    if n in cache:
        return cache[n]

    elif n <= 1:
        return 1

    else:
        cache[n] = n * find_permutations(n - 1)
        return cache[n]


if data[0] == 1:
    k = data[1]
    arr = [x for x in range(1, n + 1)]
    ans = []

    for i in range(n):
        x = find_permutations(n - 1 - i)
        step = (k - 1) // x
        ans.append(arr[step])
        arr.remove(arr[step])
        k -= x * step

    print(*ans)

else:
    input_permu = data[1:]
    sort_permu = sorted(data[1:])
    ans = 1

    for i in range(n):
        step = sort_permu.index(input_permu[i])
        sort_permu.remove(input_permu[i])
        x = find_permutations(n - 1 - i)
        ans += x * step

    print(ans)
```