---
title: "[Programmers Dev] lv1_나머지 한 점 "
excerpt: "어서와! 자료구조와 알고리즘은 처음이지?"
toc: true
toc_sticky: true
categories:
 - CS
tags:
 - 프로그래머스
 - 자료구조
 - 알고리즘
 - 문제풀이
---

## 문제풀이 lv1_나머지 한 점

[문제출처] <https://school.programmers.co.kr/courses/11947/lessons/76959>

- 주어진 세 점의 좌표를 통해 직사각형을 만들 수 있는 나머지 한 점의 좌표를 찾아낼 것

### 알고리즘 설계

1. 주어진 세 점의 좌표를 각각 x, y 좌표에 따로 리스트로 담기
2. 각 좌표 값을 count 하여 직사각형을 만들기 위해 필요한 좌표 값 얻기



### 코드 구현

```python
def solution(v):
    a,b = 0,0
    x = [ i[0] for i in v]
    y = [ i[1] for i in v]
    for i,j in v:
        if x.count(i) == 1:
            a = i
        if y.count(j) == 1:
            b = j
    return [a,b]
```



## Check Point

- count() method 의 사용