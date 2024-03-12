---
author: ["Jxun-h"]
title: "[Programmers] 광고 삽입 with Python"
date: "2021-10-17"
description: ""
summary: ""
tags: ["다이나믹프로그래밍", "PS", "DP", "알고리즘", "백준", "BOJ", "메모이제이션"]
categories: ["Algorithm"]
series: ["Programmers"]
ShowToc: false
---

<br>

## 📌 <a href="https://programmers.co.kr/learn/courses/30/lessons/72414" target="_blank">Programmers - 광고 삽입</a>

<br>

### 💡 조건 및 풀이

1.  동영상에 광고를 넣어야한다. 시청자가 가장 많은 구간에 광고를 넣어야한다.  
    = 시청자 수 구간합이 가장 큰 곳에 광고를 넣어야한다.
2.  동영상 재생시간 길이 `play_time`, 공익광고의 재생시간 길이 `adv_time`,  
    시청자들이 해당 동영상을 재생했던 구간 정보 logs
3.  **구간합을 구해 답을 이끌어내는 유형의 문제**
4.  `play_time`, `adv_time`은 길이 8로 고정된 문자열  
    `play_time`, `adv_time`은 `HH:MM:SS` 형식이며,  
    `00:00:01 <= play_time, adv_time <= 99:59:59`
5.  공익광고 재생시간은 동영상 재생시간보다 짧거나 같다.
6.  `1 <= logs <= 300000`

<br>

### 🔖 예제 및 실행결과

#### 예제

```python
print(solution("02:03:55", "00:14:15", ["01:20:15-01:45:14", "00:40:31-01:00:00", "00:25:50-00:48:29", "01:30:59-01:53:29", "01:37:44-02:02:30"]))
```

#### 실행결과

```python
"01:30:59"
```

<br>

### ⌨️ 문제 풀이

1.  play_time, adv_time (동영상 재생 길이, 광고 재생 길이)를 각각 str 타입에서 int 타입으로 변경한다.
2.  ```python
    def str_to_int(time): 
        h, m, s = time.split(':') 
        return int(h) * 3600 + int(m) * 60 + int(s)
    ```
3.  각 구간의 시청자들의 수를 기록할 배열을 만든다.
4.  ```python
    all_time = [0 for i in range(play_time + 1)]
    ```
5.  logs 를 순회하면서 시청 시작 시간에 시청자 수 + 1  
    시청 종료 시간에 시청자 수 - 1
6.  구간별 시청자 기록을 위해 all_time 배열을 순회하면서, 이전 배열의 값을 가지고 현재 배열에 더해주는 작업을 해줍니다.
7.  ```python
    for i in range(1, len(all_time)): 
        all_time[i] = all_time[i] + all_time[i - 1]
    ```
8.  모든 구간의 시청자 누적 기록을 위해 다시 한번 4번의 작업을 해줍니다.
9.  누적된 구간별 시청자 수의 정보가 저장된 배열을 순회하면서 시청자가 가장 많은 구간을 탐색합니다.
10.   
    ```python
    # 가장 시청자 수가 많은 구간을 탐색 
    for i in range(adv_time - 1, play_time): 
        # i가 공익 광고 시청 시간보다 빠를 때 
        if i >= adv_time: 
            # 지금까지 최대 누적 시청자 수가 (총 누적 시청자 수 - 해당 구간 시청자 수) 보다 작으면? 
            if most_view < all_time[i] - all_time[i - adv_time]: 
                # 지금까지 최대 누적 시청자 수를 갱신 
                most_view = all_time[i] - all_time[i - adv_time] 
                # 최대 누적 시청자 수에 해당하는 구간을 갱신 
                max_time = i - adv_time + 1 
        else: 
            # 최대 시청자 수가 현재 탐색하는 시간대의 총 누적 시청자 수보다 적을 때 
            if most_view < all_time[i]: 
                # 최대 시청자 수와 그에 해당하는 시간대를 갱신 
                most_view = all_time[i] max_time = i - adv_time + 1
    ```
11.  최대 시청자가 있는 광고 삽입 시간을 `HH:MM:SS` 형식으로 변환하여 return 합니다.

<br>

### 🖥 소스 코드

```python
def solution(play_time, adv_time, logs):
    play_time = str_to_int(play_time)

    adv_time = str_to_int(adv_time)

    all_time = [0 for i in range(play_time + 1)]

    for l in logs:
        start, end = l.split('-')

        start = str_to_int(start)
        end = str_to_int(end)

        all_time[start] += 1
        all_time[end] -= 1

    for i in range(1, len(all_time)):
        all_time[i] = all_time[i] + all_time[i - 1]

    for i in range(1, len(all_time)):
        all_time[i] = all_time[i] + all_time[i - 1]

    most_view = 0
    max_time = 0

    for i in range(adv_time - 1, play_time):

        if i >= adv_time:

            if most_view < all_time[i] - all_time[i - adv_time]:
                most_view = all_time[i] - all_time[i - adv_time]

                max_time = i - adv_time + 1
        else:

            if most_view < all_time[i]:
                most_view = all_time[i]
                max_time = i - adv_time + 1

    return int_to_str(max_time)


def str_to_int(time):
    h, m, s = time.split(':')
    return int(h) * 3600 + int(m) * 60 + int(s)


def int_to_str(time):
    h = time // 3600
    h = '0' + str(h) if h < 10 else str(h)
    time = time % 3600
    m = time // 60
    m = '0' + str(m) if m < 10 else str(m)
    time = time % 60
    s = '0' + str(time) if time < 10 else str(time)
    return h + ':' + m + ':' + s
```

<br>

### 💾 느낀점

-   문자열 타입의 시간 형식 데이터는 각 시간, 분, 초를 합쳐 숫자로 만들어 다루는 것이 편하다.
-   구간별 시청자 기록과 모든 구간의 시청자 누적 기록을 하는 부분에서 많은 이해가 필요했다.  
    스스로 이해하지 못해 다른 블로그를 참고하여 코드를 작성했다.
-   모든 구간의 시청자 누적 기록을 순회하는 부분에서도 이해가 어려워 여러번 코드를 디버깅했다.  
    이해를 하는 방향으로 코드를 보고 나의 방식으로 코드를 작성하는 시간이 필요할 것 같다.