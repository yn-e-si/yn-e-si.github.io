---
title: "[Programmers Dev] lv1_예산 소팅 "
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
use_math: true
---

## &#128161; lv1_예산 소팅

[[문제 출처]](https://school.programmers.co.kr/courses/11947/lessons/76989)

### &#128204; 문제 분석

- 부서별 신청한 예산이 주어진 리스트 d 에서 budget 값을 넘지않는 선에서 가능한 부서의 최대 개수를 리턴  

### &#128204; 알고리즘 설계

- 각각 부서의 예산 값을 담을 변수와 가능한 부서의 개수를 담을 변수 total, answer 를 선언
- 최대의 부서의 수를 구해야하기 때문에 sort 를 사용해서 loop 를 돌림
- 부서별 예산을 누적해 가면서 budget 보다 작거나 같을 때까지 부서의 개수를 더한다.

### &#128204; 코드 구현

```python
def solution(d, budget):
    total, answer = 0, 0
    for i in sorted(d):
        total += i
        if total > budget:
            break
        answer += 1
    return answer
```



## &#128161; Check Point



