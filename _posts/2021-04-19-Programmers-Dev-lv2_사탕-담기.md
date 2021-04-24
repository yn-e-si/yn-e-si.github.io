---
title: "[Programmers Dev] lv2_사탕 담기 "
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

## 문제 풀이 lv2_사탕 담기

[[문제 출처]](https://school.programmers.co.kr/courses/11947/lessons/76962)

### 문제 분석

- 가방에 사탕을 담을 수 있는 최대 무게 값과 각 사탕들에 무게가 담겨 있는 리스트가 주어진다.

- 주어진 리스트에 담긴 사탕의 무게들을 사용해서 최대 무게 값과 같아지는 경우의 수를 구하기!

- 주어진 리스트 값들의 조합을 통해 원하는 조건에 맞는 경우의 수를 구하는 문제이기에

  python 의 조합 라이브러리 사용

  > from itertools import combinations



### 알고리즘 설계

1. 주어진 전체 list 의 길이만큼 for 문 수행
   1. 전체 list 내에서의 구할 조합의 경우의 수를 조정하기 위한 for 문 수행
      1. 해당 조합의 합이 최대 무게 값과 같을 경우 answer += 1

### 코드 구현

```python
def solution(m, weights):
    answer = 0
    from itertools import combinations
    for i in range(1,len(weights)):
        for j in list(combinations(weights,i)):
            if sum(j) == m:
                answer += 1
    return answer
```



### 다른 사람 코드

```python
cnt = 0
def solution(m, weights):
    global cnt # 함수 밖에서의 변수를 호출하기에 global 선언
    if m == 0: # 재귀 함수의 종료 조건 1
        cnt += 1
    elif len(weights) == 1: # 재귀 함수의 종료 조건 2
        if m == weights[0]:
            cnt += 1
    else: # 재귀 함수 호출
        if m >= weights[0]:
            solution(m-weights[0], weights[1:])
        solution(m, weights[1:])
    return cnt
```

> 재귀 함수로 푸는 방법이 있는 줄은 생각을 못했다..(역시 세상은 넓다^^)



## Check Point

- 라이브러리의 사용도 좋지만 쓸 수 없을 경우를 대비해서 다른 방식으로도

  생각해 봐야겠다!!