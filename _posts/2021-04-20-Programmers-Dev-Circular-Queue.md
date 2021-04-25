---
title: "[Programmers Dev] 환형 큐 (Circular Queue) "
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

## 환형 큐 (Circular Queue)

: 정해진 개수의 저장 공간을 빙빙 돌려가며 이용하는 큐이다.

> 큐가 가득 차면? 
>
> 더이상 원소를 넣을 수 없다! (항상 큐 길이를 기억하고 있어야한다.)



### 환형 큐의 추상적 자료구조 구현

#### 연산 정의

- size() - 현재 큐에 들어 있는 데이터 원소의 수를 구하는 함수
- isEmpty() - 현재 큐가 비어 있는지를 판단하는 함수
- isFull() - 큐에 데이터 원소가 꽉 차 있는지를 판단하는 함수
- enqueue(x) - 데이터 원소 x 를 큐에 추가하는 함수
- dequeue() - 큐의 맨 앞에 저장된 데이터 원소를 제거 후 반환
- peek() - 큐의 맨 앞에 저장된 데이터 원소를 반환

#### 배열로 구현한 환형 큐

**예제 **- 정해진 길이 n 의 리스트를 확보해 두고 진행 (n = 6)

```python
Q.enqueue(A) -> rear = 0
Q.enqueue(B) -> rear = 1
Q.enqueue(C) -> rear = 2
Q.enqueue(D) -> rear = 3

r1 = Q.dequeue() -> front = A, r1 = A
r2 = Q.dequeue() -> front = B, r2 = B

Q.enqueue(E) -> rear = 4
Q.enqueue(F) -> rear = 5
Q.enqueue(G) -> rear = 0

r3 = Q.dequeue() -> front = C, r3 = C
```

- **front** 와 **rear** 를 적절히 계산하여 배열을 **환형으로 재활용** 한다는 것이 **환형 큐**의 핵심!!

##### 코드구현

```python
class CircularQueue:

    def __init__(self, n): # 빈 큐를 초기화
        self.maxCount = n # 인자로 주어진 최대 큐 길이 설정
        self.data = [None] * n
        self.count = 0
        self.front = -1
        self.rear = -1


    def size(self): # 현재 큐 길이를 반환
        return self.count

    def isEmpty(self): # 큐가 비어 있는지 확인
        return self.count == 0

    def isFull(self): # 큐가 꽉차 있는지 확인
        return self.count == self.maxCount

    def enqueue(self, x): # 큐에 데이터 원소 추가
        
        if self.isFull():
            raise IndexError('Queue full')
            
        self.rear = (self.rear + 1) % self.maxCount
        self.data[self.rear] = x
        self.count += 1

    def dequeue(self): # 큐에서 데이터 원소 뽑아냄
        
        if self.isEmpty():
            raise IndexError('Queue empty')
            
        self.front = (self.front + 1) % self.maxCount
        x = self.data[self.front]
        self.count -= 1
        
        return x

    def peek(self): # 큐의 맨 앞 원소 들여다 봄
        
        if self.isEmpty():
            raise IndexError('Queue empty')
            
        return self.data[(self.front + 1) % self.maxCount]



def solution(x):
    return 0
```



## Check Point