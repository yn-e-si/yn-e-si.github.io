---
title: "[Programmers Dev] 큐 (Queues) "
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

## 큐 (Queues)

: 자료 (data element) 를 보관할 수 있는 (선형) 구조이다.

  단, 넣을 때에는 한 쪽 끝에서 밀어 넣어야 한다. -> 인큐 (enqueue) 연산

  꺼낼 때에는 반대 쪽에서 뽑아 꺼내야 하는 제약이 있다. -> 디큐 (dequeue) 연산

> 선입선출 (FIFO - First - In First - Out) 특징을 가지는 선형 자료구조



### 큐의 동작

```python
Q = Queue() # 초기상태: 비어있는 큐 (empty queue)
Q.enqueue(A) # 데이터 원소 A를 큐에 추가
Q.enqueue(B) # 데이터 원소 B 를 큐에 추가
r1 = Q.dequeue() # 데이터 원소 꺼내기 -> A
r2 = Q.dequeue() # 데이터 원소 꺼내기 -> B
```

- 한쪽 방향에서 데이터가 들어가고 반대 방향에서 데이터가 나오는 구조

#### 연산의 정의

- size() - 현재 큐에 들어 있는 데이터 원소의 수를 구함
- isEmpty() - 현재 큐가 비어 있는 지를 판단
- enqueue(x) - 데이터 원소 x 를 큐에 추가
- dequeue() - 큐의 맨 앞에 저장된 데이터 원소를 제거 후 반환
- peek() - 큐의 맨 앞에 저장된 데이터 원소를 반환



### 큐의 추상적 자료구조 구현

(1) 배열 (array) 을 이용하여 구현

- Python 리스트와 메서드들을 이용 (list)

(2) 연결 리스트 (linked list) 를 이용하여 구현

- 양방향 연결 리스트 이용

#### 배열로 구현한 큐

```python
class ArrayQueue:
	def __init__(self): # 빈 큐를 초기화
		self.data = [ ]  

	def size(self): # 큐의 크기를 리턴
		return len(self.data)
	
	def isEmpty(self): # 큐가 비어 있는지 판단
		return self.size() == 0

	def enqueue(self, item): # 데이터 원소를 추가
		self.data.append(item)

	def dequeue(self): # 데이터 원소를 삭제 (리턴)
		return self.data.pop(0)

	def peek(self): # 큐의 맨 앞 원소 반환
		return self.data[0]
```

#### 배열로 구현한 큐의 연산 복잡도

- size(): O(1)

- isEmpty: O(1)

- enqueue(): O(1)

- dequeue(): O(n)

  > dequeue 연산은 queue 의 길이에 비례하는 복잡도를 가진다.

- peek(): O(1)



#### 이중 연결 리스트로 큐를 구현

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
            raise IndexError('Index out of range')

        prev = self.getAt(pos - 1)
        return self.popAfter(prev)


    def concat(self, L):
        self.tail.prev.next = L.head.next
        L.head.next.prev = self.tail.prev
        self.tail = L.tail

        self.nodeCount += L.nodeCount


class LinkedListQueue:

    def __init__(self):
        self.data = DoublyLinkedList()

    def size(self):
        return self.data.nodeCount


    def isEmpty(self):
        return self.data.nodeCount == 0


    def enqueue(self, item):
        node = Node(item)
        self.data.insertAt(self.size()+1,node)


    def dequeue(self):
        return self.data.popAt(1)


    def peek(self):
        return self.data.head.next.data



def solution(x):
    return 0
```



## Check Point





