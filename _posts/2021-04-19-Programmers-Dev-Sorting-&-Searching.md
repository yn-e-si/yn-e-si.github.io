---
title: "[Programmers Dev] 배열 - 정렬과 탐색 (Sorting & Searching) "
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

## 배열 - 정렬과 탐색 (Sorting & Searching)



### Python 리스트의 정렬

(1) sorted()

- 내장 함수이다.
- 정렬된 **새로운 리스트**를 얻어낸다.

(2) sort()

- 리스트의 메서드 (method) 이다.

- 해당 리스트를 **정렬**한다.

(3) reverse = True

- 정렬의 순서를 **반대로** 만들어 준다.
- sorted(List, reverse = True)
- List.sort(reverse = True)

```python
L = [3, 8, 2, 7, 6, 10, 9]

L2 = sorted(L)
L2
-> [2, 3, 6, 7, 8, 9, 10]

L.sort()
L
-> [2, 3, 6, 7, 8, 9, 10]

L3 = sorted(L, reverse = True)
L3
-> [10, 9, 8, 7, 6, 3, 2]

L.sort(reverse = True)
L
-> [10, 9, 8, 7, 6, 3, 2]
```



### 정렬

: 문자열로 이루어진 리스트의 경우 정렬 순서는 **사전 순서 (알파벳 순서)** 를 따름

(문자열 길이가 긴 것이 더 큰것이 아님!!)

- 문자열 길이 순서로 정렬하고 싶다면?

  -> 정렬에 이용하는 **키 (key)** 를 지정

```python
L = ['abcd', 'xyz', 'spam']
sorted(L, key = lambda x: len(x))
-> ['xyz', 'abcd', 'spam']
-> 길이가 같을 경우 원래 list 에서 앞에 있던 것이 먼저 나옴

# 키를 지정하는 또 다른 예
L = [{'name': 'John', 'score': 83}, {'name': 'Paul', 'score': 92}]
L.sort(key = lambda x: x['name'])
-> 레코드들을 이름 순서대로 정렬
L.sort(key = lambda x: x['score'], reverse = True)
-> 레코드들을 점수 높은 순으로 정렬
```



### 탐색 알고리즘 (1) - 선형탐색 (Linear Search)

: 순차적으로 진행하여 탐색하는 것

- 리스트의 길이에 비례하는 시간이 소요된다.
- 따라서 **O(n)** 의 복잡도를 가진다.
- 최악의 경우: 모든 원소를 다 비교해 보아야 한다.

```python
def linear_search(L, X):
	i = 0
	while i < len(L) and L[i] != x:
		i += 1
	if i < len(L):
		return i
	else:
		return -1
```



### 탐색 알고리즘 (2) - 이진탐색 (Binary Search)

- 탐색하려는 리스트가 이미 정렬되어 있는 경우에만 적용 가능하다.
- 크기 순으로 **정렬**되어 있다는 성질 이용할 것!

-> 한 번 비교가 일어날 때마다 **리스트 크기**를 반씩 줄임 (divide & conquer)

-> 따라서 **O(log n)** 의 복잡도를 가진다.

```python
def solution(L, x):
    answer = 0
    lower = 0
    upper = len(L) - 1
    while lower <= upper:
        middle = (lower + upper) // 2
        if L[middle] == x:
            answer = middle
            break
        elif L[middle] < x: lower = middle + 1
        else:   upper = middle - 1           
    return answer if answer else -1
```

-> 항상 이진탐색이 답일 순 없다!! **정렬에 대한 복잡도**가 고려되어야 하기 때문!!