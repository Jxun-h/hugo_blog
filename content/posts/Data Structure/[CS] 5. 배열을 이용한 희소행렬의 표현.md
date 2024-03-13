---
author: ["Jxun-h"]
title: "[CS] 5. 배열을 이용한 희소행렬의 표현"
date: "2022-07-10 02:00:00"
description: ""
summary: ""
tags: ["자료구조", "CS", "Computer Science"]
categories: ["Computer Science"]
series: ["Computer Science"]
ShowToc: false
---

<br>

## 📌 배열을 이용한 희소행렬의 표현

<br>

### 💡 희소행렬

1.  행렬의 표현
    1.  2차원 배열 : Array\[MaxRows\]\[MaxCols\]
    2.  0이 많이 포함된 경우, 희소행렬이라고 한다.
    3.  0이 아닌 데이터의 수 < 0인 데이터의 수
    4.  만약 1000 \* 1000 행렬에서 0이 아닌 원소가 10개라면, 메모리 낭비일 수 있다.

<br>

### 💡 희소행렬의 표현

1.  동기 : 공간 낭비를 줄이자.
    1.  <Row, Column, Value> 의 쌍을 저장
    2.  빠른 전치를 위해서 Row 의 오름차순으로 저장
    3.  희소행렬 -> 배열 맨 처음에 행렬의 정보기록 = (행, 열, 0이 아닌 데이터의 수)

<br>

### 💡 행렬의 전치

1.  전치연산 (Transposing a Matrix)
    1.  row & column 을 교환
    2.  <j, i, value> 를 희소행렬 M의 어디에 저장하는가?
        1.  <0, 0, 15> -> <0, 0, 15>
        2.  <0, 3, 22> -> <3, 0, 22>
        3.  <0, 5, 15> -> <5, 0, 15>
    3.  전치연산을 위한 연속적인 삽입으로 인해 기존에 저장된 항목들의 이동이 불가피 -> row 정렬이 깨져버림

<br>

### 💡 전치 연산의 구현 : Transpose

1.  Column을 기준으로 순회하면서 뒤집어 저장한다.
2.  성능분석
    1.  O(Columns \* Elements) ~ O(Columns^2 \* Rows)
    2.  복잡도 : O(Rows \* Columns)

<br>

### 💡 전치연산의 구현

1.  각 Column 이 저장될 곳을 미리 파악 -> Column index
2.  각 Column index 저장을 위한 추가적인 공간을 사용한다.
    1.  row\_terms = 2 1 2 2 0 1
    2.  starting\_pos = 1 3 4 6 8 8
3.  복잡도 : O(columns + Elements)
4.  Elements = columns \* row 일 때, Element 의 시간복잡도는 O(Columns \* Row \* Columns)