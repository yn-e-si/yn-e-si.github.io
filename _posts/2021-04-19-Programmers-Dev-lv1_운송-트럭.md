---
title: "[Programmers Dev] lv1_운송 트럭 "
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

## 문제 풀이 lv1_운송 트럭

[[문제 출처]](https://school.programmers.co.kr/courses/11947/lessons/76960)

### 문제 분석

- 주어진 최대 무게를 넘으면 트럭의 수 + 1
- 트럭에 담을 상품의 순서와 각 상품의 무게가 주어짐
- 순서에 맞게 상품을 운반하면서 이에 필요한 최소한의 트럭의 수 구하기!

### 알고리즘 설계

1. 상품의 이름과 무게가 담긴 이중리스트의 형태를 dict 형태로 변경
2. 상품의 순서가 주어진 리스트를 for 문 수행
   1. dict 와 매칭 후 최대 무게인 weight 값보다 작을 경우 무게 감소
   2. weight 값을 넘길 경우 트럭의 수 + 1
      1. weight 값을 새로 조정

### 코드구현

```python
def solution(max_weight, specs, names):
    answer = 1
    specs = { key : int(value) for key, value in specs }
    weight = max_weight
    for name in names:
        if specs[name] <= weight:
            weight -= specs[name]
        else:
            answer += 1
            weight = max_weight - specs[name]
    return answer
```



## Check Point

- weight 조정하면서 순서에 따른 error 때문에 고생했다..
- 항상 if 문에 따른 변수 값 설정 시 **실행순서** 잘 파악하기!!