---
title: "[Programmers Dev] 연결 리스트 (Linked Lists) "
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

## 연결 리스트 (Linked Lists)

일반적인 리스트와 달리 각 원소들을 줄줄이 엮어서 관리하는 자료구조이다.

각 원소를 **Node**라고 부르고 각 Node는 

값을 가지는 **data**와 다른 원소를 가리키는 **link**로 이루어져 있다.

Node

- Data - 데이터 값을 의미 한다.
- Link (next) - 다음 Node를 알려주는 주소가 담겨 있다.

-> Node 내의 데이터는 다른 구조로 이루어질 수 있다. ex) 문자열, 레코드, 다른 연결 리스트 등



※ 코드 구현의 편의성을 위해 다음의 3가지는 알 고 있는 것이 좋음! ※

- 제일 앞 Node = Head
- 제일 끝 Node = Tail
- 노드의 갯수



### 배열과 비교한 연결 리스트

배열

- 저장 공간: 연속한 위치
- 특정 원소 지칭: 매우 간편 (인덱스만 지정하면 됨)  -> 복잡도: O(1)

연결 리스트

- 저장 공간: 임의의 위치
- 특정 원소 지칭: 선형탐새고가 유사 -> 복잡도: O(n)



### 자료 구조 정의

```python
class Node:
	def __init__(self, item):
		self.data = item
		self.next = None

class LinkedList:
	def __init__(self):
		self.nodeCount = 0
		self.head = None
		self.tail = None
```



### 연산 정의

1. 특정 원소 참조 (k 번째)
2. 리스트 순회
3. 원소 삽입
4. 원소 삭제
5. 두 리스트의 연결



특정 원소 참조 (k 번째)

```python
def getAt(self, pos):
	if pos <= 0 or pos > self.nodeCount:
		return None
	i = 1
	curr = self.head
	while i < pos:
		curr = curr.next
		i += 1
        
	return curr
```

- 0 부터 시작이 아닌 1 부터 시작하는 것으로 코드를 구현했다.
- 이는 linked list 의 접근을 보다 쉽게 하기 위해서



리스트 순회

```python
class LinkedList:
    def traverse(self):
        answer = []
        curr = self.head
        
        while 1:            
            if not curr: break
            answer.append(curr.data) # 데이터 값을 출력을 위한 리스트에 저장
            curr = curr.next # 다음 값의 주소로 이동
            
        return answer
```



원소의 삽입

```python
# wrong code
def insertAt(self, pos, newNode):
	prev = self.getAt(pos-1) 
	newNode.next = prev.next
	prev.next = newNode
    
	self.Count += 1
```

- 코드 구현 주의 사항

  (1) 삽입하려는 위치가 리스트 맨 앞일 때

  	- prev 가 없다.
  	- head 의 조정이 필요하다.

  (2) 삽입하려는 위치가 리스트 맨 끝일 때

  - tail 의 조정이 필요하다.

  (3) 빈 리스트에 삽입할 때

  - (1), (2) 조건에 의해 처리가 가능하다.

```python
def insertAt(self, pos, newNode):
    # pos 가 올바른 값을 가지는 범위에 있는지 확인
    if pos < 1 or pos > self.nodeCount + 1:
        return False
    
    # pos 가 1 이면 prev 는 없고 head 는 새로운 node 를 가리키게 해줌
    if pos == 1:
        newNode.next = self.head
        self.head = newNode
        
    # 삽입하려는 위치가 처음이 아닌 경우
    else: 
        # 삽입하려는 위치가 리스트 맨 끝일 때
        if pos == self.nodeCount + 1:
            prev = self.tail
            
        else:
        	prev = self.getAt(pos - 1)
        newNode.next = prev.next
        prev.next = newNode
        
    # 삽입하려는 위치가 제일 마지막인 경우
    if pos == self.nodeCount + 1:
        self.tail = newNode
        
    self.nodeCount += 1
    
    return True
```

- 연결 리스트 원소 삽입의 복잡도
  - 맨 앞에 삽입하는 경우: O(1)
  - 중간에 삽입하는 경우: O(n)
  - 맨 끝에 삽입하는 경우: O(1) 
    - tail 을 사용하기에 상수시간이 걸리게 된다.



원소의 삭제

- 코드 구현 주의 사항

  (1) 삭제하려는 node 가 맨 앞의 것일 때

  - prev 가 없다.
  - head 의 조정이 필요하다.

  (2) 리스트 맨 끝의 node 를 삭제할 때

  - tail 의 조정이 필요하다.

```python
def popAt(self, pos):
    delete_data = self.getAt(pos)
    
    if pos < 1 or pos > self.nodeCount:
        raise IndexError
        
    elif pos == 1:
        # list의 원소가 하나이면서 첫 번째 원소를 pop 하고 싶은 경우
        if self.nodeCount == 1:
            self.head = None
            self.tail = None
        # 첫 번째 원소를 pop 하고 싶은 경우
        else:
            self.head = self.getAt(pos).next
    else:
        prev = self.getAt(pos - 1)
        prev.next = self.getAt(pos).next
        # list 의 마지막 원소를 pop 하고 싶은 경우
        if pos == self.nodeCount:
            prev.next = None
            self.tail = prev
            
    self.nodeCount -= 1
    
    return delete_data.data
```

- 연결 리스트 원소 삭제의 복잡도
  - 맨 앞에서 삭제하는 경우: O(1)
  - 중간에서 삭제하는 경우: O(n)
  - 맨 끝에서 삭제하는 경우: O(n)
    - tail 을 사용할 수 없기에 삽입과 달리 선형시간이 걸리게 된다.





두 리스트의 연결

```python
def concat(self, L):
    self.tail.next = L.head
    # 뒤에 이어 붙이는 연결 리스트가 null 일 경우를 생각해야 함
    if L.tail:
        self.tail = L.tail
        
    self.nodeCount += L.nodeCount
```



연결리스트의 장점 : 삽입과 삭제가 유연하다는 점



## 변형된 linked list

: 기존의 linked list 는 삽입과 삭제가 유연하다는 점에서 큰 장점을 갖는다.

  다만, 이는 앞에서 부터 node 를 찾으므로 시간이 오래걸린다는 단점이 있다.

  이를 해결하기 위한 방안으로 노드 자체를 기준으로 삽입, 삭제하는 메서드가 만들어 졌다.

  이 메서드는 기존과 다르게 맨 앞에서 접근을 편하게 하기 위해 리스트 head 에 의미를 갖지 않는

  **dummy node** 를 추가 생성 하였다.



### 자료 구조 정의

```python
class LinkedList:
    def __init__(self):
        self.nodeCount = 0
        self.head = Node(None)
        self.tail = None
        self.head.next = self.tail
```

- LinkedList 가 생길 때 head 가 가리키는 **dummy node** 가 추가로 생겼다.



### 연산 정의

1. 특정 원소 참조 (k 번째)
2. 리스트 순회
3. 원소 삽입
4. 원소 삭제
5. 두 리스트의 연결



특정 원소 참조 (k 번째)

```python
def getAt(self, pos):
    if pos < 0 or pos > self.nodeCount:
        return None
    ''' 
    기존 LinkedList 에서의 getAt() 함수와 달리 head 를 정의하고 dummy node 에
    0 번을 부여했기에 1 -> 0 이라는 차이점이 생김
    '''
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
    
    while curr.next:
        curr = curr.next
        result.append(curr.data)
    
    return result
```



원소의 삽입

insertAfter()

```python
def insertAfter(self, prev, newNode):
    newNodw.next = prev.next
    
    if prev.next is None:
        self.tail = newNode
        
    prev.next = newNode
    self.nodeCount += 1
    
    return True
```



insertAt()

​	(1) pos 범위 조건 확인

​	(2) pos == 1 인 경우 head 뒤에 새 node 삽입

​	(3) pos == nodeCount + 1 인 경우 tail -> prev

​	(4) 그렇지 않은 경우 getAt(..) -> prev

```python
def insertAt(self, pos, newNode):
    
    if pos < 1 or pos > self.nodeCount + 1:
        return False
    
    if pos != 1 and pos == self.nodeCount + 1:
        prev = self.tail
        
    else:
        prev = self.getAt(pos - 1)
        
    return self.insertAfter(prev, newNode)
```



원소의 삭제

- 코드 구현 주의사항

  (1) prev 가 마지막 node 일 때 (prev.next == None)

  - 삭제할 node 가 없다.

  (2) 리스트 맨 끝의 node 를 삭제할 때 (curr.next == None)

  - tail 의 조정이 필요하다.

popAfter()

```python
def popAFter(self, prev):
    curr = prev.next
    
    if prev.next == None:
        return None
    
    if curr.next == None:
        
        if self.nodeCount == 1:
            self.tail = None
            
        else:
            self.tail = prev
            
    prev.next = curr.next
    self.nodeCount -= 1
    return curr. data
```



popAt()

```python
def popAt(self, pos):
    
    if pos < 1 or pos > self.nodeCount:
        raise IndexError
        
    prev = self.getAt(pos - 1)
    
    return self.popAfter(prev)
```



두 리스트의 연결

```python
def concat(self, L):
    self.tail.next = L.head.next
    
    if L.tail:
        self.tail = L.tail
        
    self.nodeCount += L.nodeCount
```



## Check Point

