---
author: ["Jxun-h"]
title: "[CS] 1. 자료구조의 정의와 알고리즘의 정의 및 표현"
date: "2022-07-05"
description: ""
summary: ""
tags: ["자료구조", "CS", "Computer Science"]
categories: ["Computer Science"]
series: ["Computer Science"]
ShowToc: false
---

<br>

## 📌 자료구조

<br>

### 💡 정의

1.  문제해결을 위해 데이터를 조직하여 표현하는 방법
    -   전화번호부 - List, Linked List, Tree
    -   수강신청, 대기열 - Queue
    -   지하철 노선도 - Graph

<br>

### 💡 중요성

1.  주어진 문제의 특성에 맞는 자료구조를 선택한다.
    -   프로그램의 개발이 쉽고 성능이 향상한다.

<br>

### 💡 추상 데이터 타입 (Abstract Data Type)

1.  자료구조를 기술할 때 사용하는 방법

2.  데이터 객체 및 연산명세와 데이터 객체 내부 표현양식 / 연산의 구현 내용을 분리
    -   사용자가 원하는 서비스를 표현하는 부분과 서비스를 내부적으로 구현하는 부분을 분리하겠다.
        -   Ada Package, C++ Class

3.  ADT에서 연산의 명세
    -   구성요소 : 함수 이름, 인자들의 타입
    -   함수의 호출 방법 및 결과물이 무엇인지를 설명
    -   함수의 내부 동작과정 및 구현방법은 은폐

-   Information hiding
    -   서비스에 대한 유지보스나 내용이 바뀔 때, 그 서비스를 사용하는 유저에 대한 영향을 최소화 시킬 수 있다.

<br>

### 💡 알고리즘의 정의

1.  문제 해결을 위해 특정한 일을 수행하는 명령어들의 집합

<br>

### 💡 알고리즘이 만족해야할 조건

1.  입력(Input) : 0 혹은 그 이상의 입력이 존재해야한다.
2.  출력(Output) : 적어도 하나 이상의 결과물이 출력되어야한다.
3.  명확성(Defineteness) : 알고리즘을 구성하는 명령어들의 의미는 명확해야하며, 애매모호해서는 안된다.
4.  유한성(Finiteness) : 알고리즘은 한정된 수의 명령어들을 실행한 후 종료해야한다.
5.  유효성/실행 가능성(Effectiveness) : 모든 명령어들은 실행가능해야한다.
    -   코끼리 냉장고에 넣기 (명확성)
        -   냉장고 문열기
        -   코끼리 넣기 (실행가능성 X)
        -   문 닫기위의 세가지는 유한성을 만족한다.