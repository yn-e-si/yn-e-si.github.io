---
title: "[Programmers Dev] 이진 탐색 트리 (Binary Search Trees) "
excerpt: "어서와! 자료구조와 알고리즘은 처음이지?"
toc: true
toc_sticky: true
categories:
 - CS
tags:
 - 프로그래머스
 - 자료구조
 - 알고리즘
use_math: true
---

## &#128161; 이진 탐색 트리 (Binary Search Trees)

### &#128204; 정의

![](https://yn-e-si.com/assets/images/program_dev/tree_8.JPG){: .align-center}

모든 노드에 대해서

- 왼쪽 서브트리에 있는 데이터는 모두 현재 노드의 값보다 작고
- 오른쪽 서브트리에 있는 데이터는 모두 현재 노드의 값보다 큰

성질을 만족하는 이진트리이다.

<br/>

### (정렬된) 배열을 이용한 이진 탐색과 비교한 이진 탐색 트리

장점: 데이터 원소의 추가, 삭제가 용이하다.

단점: 공간 소요가 크다.

> &#128173; 이진 탐색 트리는 항상 $O(log n)$ 을 갖는 것은 아니다.

<br/>

### 이진 탐색 트리의 추상적 자료구조

#### 데이터 표현

- 각 노드는 (key, value) 의 쌍으로 이루어져 있다.
- key 를 이용해서 검색이 가능하다.
- 보다 복잡한 데이터 레코드로 확장이 가능하다.



#### 연산의 정의

- <code>insert(key, data)</code> - 트리에 주어진 데이터 원소를 추가한다.
- <code>remove(key)</code> - 특정 원소를 트리로부터 삭제한다.
- <code>lookup(key)</code> - 특정 원소를 검색한다.
- <code>inorder()</code> - 키의 순서대로 데이터 원소를 나열한다.
- <code>min(), max()</code> - 최소 키, 최대 키를 가지는 원소를 각각 탐색한다.



#### 코드 구현

##### Node

<code>초기화</code>

```python
class Node:
	# 초기화
	def __init__(self, key, data):
		self.key = key
		self.data = data
		self.left = None
		self.right = None
```

<br/>

<code>inorder()</code>

```python
# in - order traversal
	def inorder(self):
		traversal = []
		if self.left():
			traversal += self.left.inorder()
		traversal.append(self)
		if self.right:
			traversal += self.right.inorder()
		return traversal
```

<br/>

<code>min()</code>

```python
# min()
	def min(self):
		if self.left:
			return self.left.min()
		else:
			return self
```

<br/>

<code>max()</code>

```python
# max()
	def max(self):
		if self.right:
			return self.right.max()
		else:
			return self
```

<br/>

<code>lookup()</code>

```python
# lookup()
# 입력 인자: 찾으려는 대상 키
# 리턴: 찾은 노드와, 그것의 부모 노드 ( 각각, 없으면 None 으로 ) 

	def lookup(self, key, parent = None):
		if key < self.key : 
			if self.left:
				return self.left.lookup(key, self)
			else:
				return None, None
		elif key > self.key:
			if self.rignt:
				return self.right.lookup(key, self)
			else:
				return None, None
		else:
			return self, parent
```

<br/>

<code>insert()</code>

```python
# insert()
# 입력 인자: 키, 데이터 원소
# 리턴: 없음

	def insert(self, key, data):
		if key < self.key:
			if self.left:
	    		self.left.insert(key, data)
     		else:
        		self.left = Node(key, data)
    	elif key > self.key:
			if self.right:
	    		self.right.insert(key, data)
    		else:
	    		self.right = Node(key, data)
    	else:
			raise KeyError("Key Error")
    	return True
```

<br/>

<code>countChildren()</code>

```python
# countChildren()
# 리턴: 자식의 수
	def countChildren(self):
        count = 0
        if self.left:
            count += 1
        if self.right:
            count += 1
        return count
```

<br/>

##### BinSearchTree

<code>초기화</code>

```python
class BinSearchTree:
	# 초기화
		def __init__(self):
			self.root = None
```

<br/>

<code>inorder()</code>

```python
# in - order traversal
	def inorder(self):
		if self.root:
			return self.root.inorder()
		else:
			return []
```

<br/>

<code>min()</code>

```python
# min()
	def min(self):
		if self.root:
			return self.root.min()
		else:
			return None
```

<br/>

<code>max()</code>

```python
# max()
	def max(self):
		if self.root:
			return self.root.max()
		else:
			return None
```

<br/>

<code>lookup()</code>

```python
# lookup()
# 입력 인자: 찾으려는 대상 키
# 리턴: 찾은 노드와, 그것의 부모 노드 ( 각각, 없으면 None 으로 ) 
	def lookup(self, key):
		if self.root:
			return self.root.lookup(key)
		else:
			return None, None
```

<br/>

<code>insert()</code>

```python
# insert()
# 입력 인자: 키, 데이터 원소
# 리턴: 없음
	def insert(self, key, data):
		if self.root:
			self.root.insert(key, data)
		else:
			self.root = Node(key, data)
```

<br/>

##### 이진 탐색 트리에서 원소 삭제

1. 키 (key) 를 이용해서 노드를 찾는다.
   - 해당 키의 노드가 없으면, 삭제할 것도 없음
   - 찾은 노드의 부모 노드도 알고 있어야 한다.
2. 찾은 노드를 제거하고도 이진 탐색 트리 성질을 만족하도록 트리의 구조를 정리한다.

<br/>

##### 이진 탐색 트리 구조의 유지

- 삭제되는 노드가
  - 말단 (leaf) 노드인 경우
  - 자식을 하나 가지고 있는 경우
  - 자식을 둘 가지고 있는 경우

1.말단 (leaf) 노드인 경우

- leaf 노드를 없애면 된다.

> &#128173; 부모 노드의 링크를 조정한다. (좌 or 우)
>
> &#128173; 삭제되는 노드 (X) 가 root node 인 경우는 트리 전체가 없어지는 코드를 짜야한다.

<br/>

2.자식을 하나 가지고 있는 경우

- 삭제되는 노드 자리에 그 자식을 대신 배치한다.

> &#128173; 자식이 왼쪽 오른쪽이냐에 따라 달라지고, 부모 노드의 링크를 조정한다. (좌 or 우)
>
> &#128173; 삭제되는 노드 (X) 가 root node인 경우는 대신 들어오는 자식이 새로 root node 가 된다.

<br/>

3.자식을 둘 가지고 있는 경우

- 삭제되는 노드보다 바로 다음 (큰) 키를 가지는 노드를 찾아 그 노드를 삭제되는 노드 자리에 대신 배치하고 이 노드를 대신 삭제한다.

<br/>

<code>remove()</code>

```python
# remove()
# 입력 인자: 키
# 리턴: 삭제한 경우 True, 해당 키의 노드가 없는 경우 False
class BinSearchTree:
    def remove(self, key):
        # 삭제하려는 노드와 parent를 검색
    	node, parent = self.lookup(key)
        
        # 삭제하는 노드가 존재한다면
        if node:
            
            # 자식노드의 개수가 몇 개인지 확인
            nChildren = node.countChildren()
            
            # The simplest case of no children
            if nChildren == 0:
                
                # 만약 parent 가 있으면
                # node 가 왼쪽 자식인지 오른쪽 자식인지 판단하여
                # parent.left 또는 parent.right 를 None 으로 하여
                # leaf node 였던 자식을 트리에서 끊어내어 없앱니다.
                if parent:
                    if parent.left == node:
                        parent.left = None
                    else:
                        parent.right = None
                        
                # 만약 parent 가 없으면 (node 는 root 인 경우)
                # self.root 를 None 으로 하여 빈 트리로 만듭니다.
                else:
                    self.root = None
                    
            # When the node has only one child
            elif nChildren == 1:
                
                # 하나 있는 자식이 왼쪽인지 오른쪽인지를 판단하여
                # 그 자식을 어떤 변수가 가리키도록 합니다.
                if node.left:
                    successor = node.left
                else:
                    successor = node.right
                    
                # 만약 parent 가 있으면
                # node 가 왼쪽 자식인지 오른쪽 자식인지 판단하여
                # 위에서 가리킨 자식을 대신 node 의 자리에 넣습니다.
                if parent:
                    if parent.left == node:
                        parent.left = successor
                    else:
                        parent.right = successor
                        
                # 만약 parent 가 없으면 (node 는 root 인 경우)
                # self.root 에 위에서 가리킨 자식을 대신 넣습니다.
                else:
                    self.root = successor
                    
            # When the node has both left and right children
            else:
                parent = node
                successor = node.right
                
                # parent 는 node 를 가리키고 있고,
                # successor 는 node 의 오른쪽 자식을 가리키고 있으므로
                # successor 로부터 왼쪽 자식의 링크를 반복하여 따라감으로써
                # 순환문이 종료할 때 successor 는 바로 다음 키를 가진 노드를,
                # 그리고 parent 는 그 노드의 부모 노드를 가리키도록 찾아냅니다.
                while successor.left:
                    parent = successor
                    successor = successor.left
                    
                # 삭제하려는 노드인 node 에 successor 의 key 와 data 를 대입합니다.
                node.key = successor.key
                node.data = successor.data
                
                # 이제, successor 가 parent 의 왼쪽 자식인지 오른쪽 자식인지를 판단하여
                # 그에 따라 parent.left 또는 parent.right 를
                # successor 가 가지고 있던 (없을 수도 있지만) 자식을 가리키도록 합니다.
                if parent.left == successor:
                    parent.left = successor.right
                else:
                    parent.right = successor.right

            return True

        else:
            return False

```

<br/>

#### 이진 탐색 트리가 별로 효율적이지 못한 경우

```python
T = BinSearchTree()
T.insert(1, 'John')
T.insert(2, 'Marry')
T.insert(3, 'Anne')
T.insert(4, 'Peter')
```

- 이진 탐색 트리이긴 하나 한쪽으로 치우처져 있고 균형이 잡혀있지 않다.
- 따라서 선형 탐색과 동등한 정도의 복잡도를 가지게 된다.

> &#128173; 높이의 균형을 맞추지 못하고 한쪽으로 치우쳐져 있는 경우라서 효율적이지 못한 것이다. 높이가 비슷하면서 왼쪽 오른쪽이 어느 정도 균형이 잡힌 트리여야 효율적이다.

<br/>

#### 보다 나은 성능을 보이는 이진 탐색 트리들

- 높이의 균형을 유지함으로써 $O(logn)$ 의 탐색 복잡도를 보장하는 장점이 있다.
- 삽입, 삭제 연산이 보다 복잡해지는 단점이 있다.
- 추가적으로 [AVL tree](https://ko.wikipedia.org/wiki/AVL_트리), [Red-black tree](https://ko.wikipedia.org/wiki/레드-블랙_트리) 에 대해서 알아보면 좋다.

<br/>

<br/>

## &#128161; Check Point

- 이진 탐색 트리 핵심 연산인 탐색, 삽입, 삭제의 계산복잡도는 $O(h)$ 으로 트리의 높이에 의해 수행 시간이 결정되는 구조이다.
- 균형이 잡혀있다면 탐색 복잡도가 $O(logn)$ 이지만 균형이 잡혀있지 않다면 $O(n)$ 의 복잡도를 가지는 단점이 있다.