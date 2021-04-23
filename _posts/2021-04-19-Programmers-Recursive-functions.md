---
title: "[Programmers Dev] 재귀 알고리즘 (Recursive functions) "
excerpt: "어서와! 자료구조와 알고리즘은 처음이지?"
toc: true
toc_sticky: true
categories:
 - CS
tags:
 - 프로그래머스
 - 자료구조
 - 알고리즘
---

## 재귀 알고리즘 - 기초

### 재귀함수 (recursive functions) 란?

: 하나의 함수에서 **자신을 다시 호출**하여 작업을 수행하는 것을 말한다.

- 생각보다 많은 종류의 문제가 재귀적으로 해결 가능

- ex) 이진 트리 (binary trees), 자연수의 합 구하기

```python
문제: 1부터 n까지 모든 자연수의 합을 구하시오.

def sum(n):
	return n + sum(n-1)

-> 끝내는 조건이 없기에 에러!

def sum(n):
	if n<=1: return n
	else: return n + sum(n-1)
    
-> 재귀 호출의 종결 조건이 엄청 중요함!!
```



### 재귀 알고리즘의 효율

- 모든 Recursive algorithm 은 그에 맞는 Iterative algorithm 이 존재한다.

- 효율적인 측면에서 보면 Recursive version 이 **n 이 커질수록** 계속해서 함수를

  호출하게 되어 Iterative version 보다 **효율성**이 떨어진다.

- 복잡도 측면에서는 두 개의 version 이 **똑같다**.

```python
# Recursive version
def sum(n):
	if n<=1:
		return n
	else:
		return n + sum(n-1)
-> O(n)

# Iterative version
def sum(n):
	s=0
	while n>=0:
		s += n
		n -= 1
	return s
-> O(n)

```

```python
# n! 를 구하는 재귀 함수
def what(n):
    if n <= 1:
        return 1
    else:
        return n * what(n - 1)
```

- 이처럼 재귀 함수는 **직관적**으로 이해하기에 좋음



```python
연습문제 - Fibonacci 순열

# Recursive version
def solution(x):
    if x == 0: return 0
    if x == 1: return 1
    return solution(x-1) + solution(x-2)

# Iterative version
def solution(x):
    n1 = 0
    n2 = 1
    i = 1
    n = 0 
    while i<x:
        n = n1 + n2
        n1 = n2
        n2 = n
        i += 1  
    return 1 if x == 1 else n
```



## 재귀 알고리즘 - 응용

```python
문제: n 개의 서로 다른 원소에서 m 개를 택하는 경우의 수
    
nCm = (n-1)C(m) + (n-1)C(m-1)
- 특정한 하나의 원소 입장에서 볼 때
- 이 원소를 포함하는 경우
- 그렇지 않은 경우를 따로 계산해서 더해야함

# 내장함수 사용
from math import fatorial as f

def combi(n, m):
    return f(n) / (f(m) * f(n - m))

# recursive version
def combi(n, m):
    return combi(n - 1, m) + combi(n - 1, m - 1)

-> trivial case를 고려하지 않은 case
-> 위와 같이 만들 시 error 발생!!

def combi(n, m):
    if n == m: # trivial case
        return 1
    elif m == 0: # trivial case
        return 1
    else:
        return combi(n - 1, m) + combi(n - 1, m - 1)
    
-> 효율성 측면에서 n이 커지면 함수를 여러번 호출되는 상황이 오므로
   n이 커질수록 효율성이 떨어지는 측면이 있다!

```

```python
연습문제 - 재귀적 이진 탐색

def solution(L, x, l, u):
    if l > u:
        return -1
    mid = (l + u) // 2
    if x == L[mid]:
        return mid
    elif x < L[mid]:
        return solution(L, x, l, mid - 1)
    else:
        return solution(L, x, mid + 1, u)
```



## Check Point

- Recursive Algorithm은 **직관적**으로 이해하기에 좋다.
- 단, 항상 **trivial case (종결 조건)** 을 신경써야 함!! 
-  효율성 측면에서 **n이 커질 수록** Iterative Algorithm보다 떨어진다.