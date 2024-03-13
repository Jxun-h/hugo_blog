---
author: ["Jxun-h"]
title: "[CS] 7. 연결리스트를 이용한 다항식의 구현"
date: "2022-07-10 04:00:00"
description: ""
summary: ""
tags: ["자료구조", "CS", "Computer Science"]
categories: ["Computer Science"]
series: ["Computer Science"]
ShowToc: false
---

<br>

## 📌 연결리스트를 이용한 다항식의 구현

<br>

### 💡 다항식의 연결리스트 표현

1.  다항식의 구조체

```c++
struct poly{
    int coef;           // 계수
    int expon;          // 지수
    struct poly *link;  // 링크

}*a, *b, *c
```

<br>
<center><img src='/cs_7_1.png' /></center>

<br>

### 💡 다항식의 덧셈 알고리즘

1.  d = a + b
    1.  각 다항식 최고차 항부터 차례대로 비교하며 연산

2.  최고차 항의 지수가 동일할 경우

<center><img src='/cs_7_2.png' /></center>
