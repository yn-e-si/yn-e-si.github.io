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
3. 길이 얻어내기
4. 원소 삽입
5. 원소 삭제
6. 두 리스트의 합치기



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

```

- 연결 리스트 원소 삭제의 복잡도
  - 맨 앞에서 삭제하는 경우: O(1)
  - 중간에서 삭제하는 경우: O(n)
  - 맨 끝에서 삭제하는 경우: O(n)
    - tail 을 사용할 수 없기에 삽입과 달리 선형시간이 걸리게 된다.