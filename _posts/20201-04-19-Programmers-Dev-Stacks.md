---
title: "[Programmers Dev] 스택 (Stacks) "
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

## 스택 (Stacks)

- 자료 (data element) 를 보관할 수 있는 (선형) 구조이다.
- 넣을 때에는 한 쪽 끝에서 밀어서 넣게 되는 **푸시 (push)** 연산을 하게 된다.
- 꺼낼 떄에는 같은 쪽에서 뽑아 꺼내야 하는 **팝 (pop)** 연산이 있다.

>**후입선출 (LIFO: Last - In - First - Out)** 특징을 가지는 선형 자료구조



스택의 동작

```python
S = Stack() # 초기 상태: 비어 있는 스택
S.push(A) # 데이터 원소 A 를 스택에 추가
S.push(B) # 데이터 원소 B 를 스택에 추가
r1 = S.pop() # 가장 마지막에 들어간 데이터 원소 B 를 꺼냄
r2 = S.pop() # 가장 위에 남은 데이터 원소 A 를 꺼냄

# 비어 있는 스택에서 데이터 원소를 꺼낼 경우 에러 발생: 스택 언더플로우
r3 = S.pop()

# 꽉
```

- 비어 있는 스택에서 데이터 원소를 꺼낼 경우 에러 발생: **스택 언더플로우**
- 꽉 찬 스택에 데이터 원소를 넣으려 할 때 에러 발생: **스택 오버플로우**



### 스택의 추상적 자료구조 구현

(1) 배열 (array) 을 이용하여 구현

- Python 리스트와 메서드들을 이용

(2) 연결 리스트 (linked list) 를 이용하여 구현

- 양방향 연결 리스트 이용



### 연산의 정의

- size() - 현재 스택에 들어 있는 데이터 원소의 수를 구함
- isEmpty() - 현재 스택이 비어 있는지를 판단
- push(x) - 데이터 원소 x 를 스택에 추가
- pop() - 스택의 맨 위에 저장된 데이터 원소를 제거 후 반환
- peek() - 스택의 맨 위에 저장된 데이터 원소를 반환



배열로 구현한 스택

```python
class ArrayStack:
	def __init__(self): # 빈 스택을 초기화
		self.data = [] 
        
	def size(self): # 스택의 크기를 리턴
		return len(self.data) 
    
	def isEmpty(self): # 스택이 비어있는지 판단
		return self.size() ==0 
    
	def push(self, item): # 데이터 원소를 추가
		self.data.append(item)
        
	def pop(self): # 데이터 원소를 삭제 (리턴)
		return self.data.pop()
    
	def peek(self): # 스택의 꼭대기 원소 반환
		return self.data[-1]
```



양방향 연결 리스트로 구현한 스택

```python
class LinkedListStack:
	def __init__(self): # 빈 스택을 초기화
		self.data = DoublyLinkedList()

	def size(self): # 스택의 크기를 리턴
		return self.data.getLength()

	def isEmpty(self): # 스택이 비어있는지 판단
		return self.size() == 0

	def push(self, item): # 데이터 원소를 추가
		node = Node(item)
		self.data.insertAt(self.size() + 1, node)

	def pop(self): # 데이터 원소를 삭제 (리턴)
		return self.data.popAt(self.size())

	def peek(self): # 스택의 꼭대기 원소 반환
		return self.data.getAt(self.size()).data
```



라이브러리 패키지로 구현한 스택

```python
from pythonds.basic.stack import Stack
S = Stack()
dir(s)
> isEmpty, items, peek, pop, push, size... 
```

- 이미 만들어진 메소드들을 사용할 수 있음



### 연습문제 - 수식의 괄호 유효성 검사

**알고리즘 설계**

 - 수식을 왼쪽부터 한 글자씩 읽어서:
 - 여는 괄호 '(' 또는 '{' 또는 '[' 를 만나면 스택에 푸시
 - 닫는 괄호 ')' 또는 '}' 또는 ']' 를 만나면:
   - 스택이 비어 있으면 올바르지 않은 수식
   - 스택에서 pop, 쌍을 이루는 여는 괄호인지 검사
     - 맞지 않으면 올바르지 않은 수식

> 올바른 수식:
> - (A + B)
> - {(A + B) * C}
> - [(A + B) * (C + D)]
>
> 올바르지 않은 수식:
> - (A + B
> - A + B)
> - {A * (B + C})
> - [(A + B) * (C + D)}



**코드 구현**

``` python
class ArrayStack:

    def __init__(self):
        self.data = []

    def size(self):
        return len(self.data)

    def isEmpty(self):
        return self.size() == 0

    def push(self, item):
        self.data.append(item)

    def pop(self):
        return self.data.pop()

    def peek(self):
        return self.data[-1]


def solution(expr):
    match = {
        ')': '(',
        '}': '{',
        ']': '['
    }
    S = ArrayStack()
    for c in expr:
        if c in '({[':
            S.push(c)

        elif c in match:
            if S.isEmpty():
                return False
            else:
                t = S.pop()
                if t != match[c]:
                    return False
    return S.isEmpty()
```



## Check Point

- 스택은 **후입선출 (LIFO)** 구조를 갖는 선형 자료구조이다.

- list, DoublyLinkedList, 라이브러리 패키지로 구현이 가능하다.
- 코테에 빈번하게 사용하니 쓰임에 있어 **익숙**해질 것!!