---
title: "[Programmers Dev] 우선순위 큐 (Priority Queues) "
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

## &#128161; 우선순위 큐 (Priority Queues)

큐가 **FIFO (First - In First - Out) 방식**을 따르지 않고 원소들의 **우선순위**에 따라

큐에서 빠져나오는 방식

<br/>



**[예제]** 값이 작은 것이 우선순위가 있다고 가정

Enqueue - 6, 7, 3, 2

Dequeue - 2 3 6 7



### 우선순위 큐의 활용

- 운영체제의 CPU 스케줄러

### 우선순위 큐의 구현

- 서로 다른 두 가지 방식이 가능:
  1. enqueue 할 때, 우선순위 순서를 유지하도록
  2. dequeue 할 때, 우선순위 높은 것을 선택

> &#128173; 1 이 좀 더 유리하다. 2 일 경우, 정렬이 안되어 있는 것이므로 모든 값을 다 찾아봐야 하기 때문!

- 서로 다른 두 가지 재료 이용 가능:
  1. 선형 배열 이용
  2. 연결 리스트 이용

> &#128173; 시간적으로 볼 때는 연결 리스트를 이용하는 것이 유리하다. 보통 양 끝이 아닌 중간부분에 데이터를 삽입하려는 일이 빈번하게 일어나는데 이를 연결 리스트가 효과적으로 수행이 가능하다. 다만, 공간의 소요를 볼 때는 선형 배열이 덜 사용하게 된다.



<br/>

**기존의 양방향 연결 리스트 선언**

```python
class Node:

    def __init__(self, item):
        self.data = item
        self.prev = None
        self.next = None


class DoublyLinkedList:

    def __init__(self):
        self.nodeCount = 0
        self.head = Node(None)
        self.tail = Node(None)
        self.head.prev = None
        self.head.next = self.tail
        self.tail.prev = self.head
        self.tail.next = None


    def __repr__(self):
        if self.nodeCount == 0:
            return 'LinkedList: empty'

        s = ''
        curr = self.head
        while curr.next.next:
            curr = curr.next
            s += repr(curr.data)
            if curr.next.next is not None:
                s += ' -> '
        return s


    def getLength(self):
        return self.nodeCount


    def traverse(self):
        result = []
        curr = self.head
        while curr.next.next:
            curr = curr.next
            result.append(curr.data)
        return result


    def reverse(self):
        result = []
        curr = self.tail
        while curr.prev.prev:
            curr = curr.prev
            result.append(curr.data)
        return result


    def getAt(self, pos):
        if pos < 0 or pos > self.nodeCount:
            return None

        if pos > self.nodeCount // 2:
            i = 0
            curr = self.tail
            while i < self.nodeCount - pos + 1:
                curr = curr.prev
                i += 1
        else:
            i = 0
            curr = self.head
            while i < pos:
                curr = curr.next
                i += 1

        return curr


    def insertAfter(self, prev, newNode):
        next = prev.next
        newNode.prev = prev
        newNode.next = next
        prev.next = newNode
        next.prev = newNode
        self.nodeCount += 1
        return True


    def insertAt(self, pos, newNode):
        if pos < 1 or pos > self.nodeCount + 1:
            return False

        prev = self.getAt(pos - 1)
        return self.insertAfter(prev, newNode)


    def popAfter(self, prev):
        curr = prev.next
        next = curr.next
        prev.next = next
        next.prev = prev
        self.nodeCount -= 1
        return curr.data


    def popAt(self, pos):
        if pos < 1 or pos > self.nodeCount:
            return None

        prev = self.getAt(pos - 1)
        return self.popAfter(prev)


    def concat(self, L):
        self.tail.prev.next = L.head.next
        L.head.next.prev = self.tail.prev
        self.tail = L.tail

        self.nodeCount += L.nodeCount

```

<br/>

**우선순위 큐의 초기화**

```python
from doublylinkedlist import Node, DoublyLinkedList

class PriorityQueue: # 양방향 연결 리스트를 이용하여 빈 큐를 초기화
	def __init__(self, x):
		self.queue = DoublyLinkedList()

```

> &#128173; 양방향 연결 리스트의 getAt() 메서드를 이용하지 않는다. getAt() 는 포지션이 주어졌을 때, 매번 그 포지션을 세어 나가기에 효율이 좋지 않다.

<br/>

**큐의 길이**

```python
def size(self):
    return self.queue.getLength()
```

<br/>

**빈 큐인지 확인**

```python
def isEmpty(self):
    return self.size() == 0
```

<br/>

**원소 삽입**

```python
def enqueue(self, x):
    newNode = Node(x)
    curr = self.queue.head

    while curr.next != self.queue.tail and x < curr.next.data:
        curr = curr.next
        
    self.queue.insertAfter(curr, newNode)

```

<br/>

**원소 삭제**

```python
def dequeue(self):
    return self.queue.popAt(self.queue.getLength())
```

<br/>

**큐의 맨 앞 원소 확인**

```python
def peek(self):
    return self.queue.getAt(self.queue.getLength()).data
```



<br/>

<br/>

## &#128161; Check Point

- 일반적인 큐와 달리 **우선순위**에 따라 원소들을 관리한다.