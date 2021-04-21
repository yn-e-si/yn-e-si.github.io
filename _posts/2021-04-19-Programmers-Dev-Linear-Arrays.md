---
title: "[Programmers Dev] 선형 배열 (Linear Arrays) "
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

## 선형 배열 ( Linear Arrays)

배열 (Arrays): 같은 종류의 데이터가 줄지어 있는 것

리스트 (Lists): 파이썬에서 제공하는 배열 자료구조

-> Python 에서의 리스트는 다른 언어에서의 배열과 달리 <u>서로 다른 타입의 원소</u>들도 하나의 리스트 안에 넣을 수가 있다!



### 리스트 (배열) 연산

``` python
# (1) 원소 덧붙이기
L = ['Bob', 'Cat', 'Spam', 'Programmers']
L.append('New')
-> ['Bob', 'Cat', 'Spam', 'Programmers', 'New']

# (2) 끝에서 꺼내기
L.pop() -> 'New'
-> ['Bob', 'Cat', 'Spam', 'Programmers']

# (3) 원소 탐색하기
L = ['Bob', 'Cat', 'Spam', 'Programmers']
L.index('Spam')
-> 2
```

-> **append(), pop(), index()** method 는 수행시간이 리스트의 길이와 <u>무관</u>하다. (상수 시간)

->따라서 **O(1)** 의 복잡도를 가진다.



```python
# (3) 원소 삽입하기
L = [20, 37, 58, 72, 91]
L.insert(3, 65): index 3 의 위치에 65 를 삽입
-> [20, 37, 58, 65, 72, 91]

# (4) 원소 삭제하기
del(L[2]): 리스트 L 의 index 2 의 위치 원소를 삭제
-> [20, 37, 65, 72, 91]
```

-> **insert(), del()** method는 수행시간이 리스트의 길이와 <u>비례</u>한다. (선형 시간)

-> 이는 삽입 및 삭제 후 리스트 내의 원소들을 다시 이동시켜주어야 하기 때문!

-> 따라서 **O(n)** 의 복잡도를 가진다.



### 서로 다른 복잡도른 가지는 del 과 pop 의 차이점

- pop 은 리스트의 맨 마지막 원소를 제거한다.
- del 은 제거하고 싶은 인덱스를 입력 후 제거한다.



### 연습문제

```python
(1) 정렬된 리스트에 주어진 원소 삽입하기

def solution(L, x):
    for i in range(len(L)):
        if L[i] > x: # 앞에서부터 순차적으로 비교
            L.insert(i, x)
            break
        if L[-1] < x: # 효율성을 위해 주어진 원소가 제일 큰 값일 경우를 고려
            L.insert(len(L), x)
            break
    return L

(2) 주어진 리스트에서 특정 원소를 모두 찾아내라.

def solution(L, x):
    answer = []
    for i in range(len(L)):
        if L[i] == x:
            answer.append(i)
    return answer if answer else [-1]
```

