---
title: "[Programmers Dev] 양방향 연결 리스트 (Doubly Linked Lists) "
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

## 양방향 연결 리스트 (Doubly Linked Lists)

- 한 쪽으로만 링크를 연결한 것이 아닌, 양쪽으로 연결한 자료구조
- 앞으로도 (다음 node) 뒤로도 (이전 node) 진행이 가능하다.



## 자료 구조 정의

```python
# node 의 구조 확장
class Node:
    
    def __init__(self, item):
        
        self.data = item
        self.prev = None
        self.next = None

class DoublyLinkedList:
    
    def __init__(self, item):
        
        self.nodeCount = 0
        self.head = Node(None)
		self.tail = Node(None)
        self.head.prev = None
        self.head.next = self.tail
        self.tail.prev = self.head
        self.tail.next = None
```

- 리스트 처음과 끝에 dummy node 를 생성
- 데이터를 담고 있는 node 들이 모두 같은 모양을 가짐



### 연산 정의

1. 특정 원소 참조 (k 번째)
2. 리스트 순회
3. 원소 삽입
4. 원소 삭제
5. 두 리스트의 연결



특정 원소 참조 (k 번째)

```python
# 코드 개선 전 
def getAt(self, pos):
    
	if pos < 0 or pos > self.nodeCount:
		return None
	i = 0
	curr = self.head
    
	while i < pos:
		curr = curr.next
		i += 1
        
	return curr
```

```python
# 코드 개선 - 리스트 마지막에 원소 삽입하는 상황을 고려
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
```



리스트 순회

```python
def traverse(self):
    
    result = []
    curr = self.head
    # tail 에도 Node 가 존재하기에 next.next 까지 살펴보는 것
    while curr.next.next:
        
        curr = curr.next
        result.append(curr.data)
        
    return result
```



리스트 역순회

```python
def reverse(self):
    
	result = []
	curr = self.tail
    
	while curr.prev.prev:
        
		curr = curr.prev
		result.append(curr.data)
        
	return result
```



원소의 삽입

```python
def insertAfter(self, prev, newNode):
    
	next = prev.next
	newNode.prev = prev
	newNode.next = next
	prev.next = newNode
	next.prev = newNode
	self.nodeCount += 1
    
	return True

def insertBefore(self, next, newNode):
    
        prev = next.prev
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

```



원소의 삭제

```python
def popAfter(self, prev):
    
    next = prev.next.next
    delete_node = prev.next
    prev.next = next
    next.prev = prev
    self.nodeCount -= 1
        
    return delete_node.data

def popBefore(self, next):
    
    prev = next.prev.prev
    delete_node = next.prev
    prev.next = next
    next.prev = prev
    self.nodeCount -= 1
        
    return delete_node.data

def popAt(self, pos):
    
    if pos < 1 or pos > self.nodeCount:
        
        raise IndexError
        
    else:
        
        prev = self.getAt(pos - 1)
        
        return self.popAfter(prev)
```

- 양방향 연결 리스트는 링크가 차지하는 메모리 용량이 늘어났지만 코딩이 편해진다.



두 리스트의 연결

```python
def concat(self, L):
    
    self.tail.prev.next = L.head.next
    L.head.next.prev = self.tail.prev
    seilf.tail = L.tail
    self.nodeCount += L.nodeCount
```



## Check Point

- 기존의 linked list 보다 개선된 형태이다.
- linked list 양 쪽 끝에 **dummy node** 를 만듬으로써 **양쪽**으로 진행 가능한 형태이다.
- **코딩구현 및 접근**이 용이하지만 차지하는 **메모리 용량**이 늘어났다는 단점도 또한 존재한다.