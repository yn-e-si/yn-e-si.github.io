---
title: "[Programmers Dev] 트리 (Trees) "
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

## &#128161; 트리 (Trees)

정점 (node) 과 간선 (edge) 을 이용하여 데이터의 배치 형태를 추상화한 자료구조이다.

- 2차원의 자료 구조
- 정보를 조직화하고 검색하는데 용이하게 이용 가능

<br/>

### &#128204; 용어 정리

![](https://yn-e-si.com/assets/images/program_dev/tree_1.JPG){: .align-center}

<br/>

- 루트 (Root) 노드: 제일 위에 위치한 노드 - A
- 리프 (Leaf) 노드: 더 이상 가지칠 수가 없는 맨 밑에 있는 노드 - H, I, J
- 내부 (Internal) 노드: 루트오 리프도 아닌 중간에 있는 노드 - B, C, D, E, F, G
- 부모 (Parenet) 노드: 간선으로 연결된 노드들 사이에서 루트 노드 쪽에 가까운 노드 - 간선으로 연결된 D, H, I 의 관계에서 보면 D 가 H, I 의 부모 노드이다.
- 자식 (Child) 노드: 간선으로 연결된 노드들 사이에서 리프 노드 쪽에 가까운 노드 - D, H, I 관계에서 H, I 가 D 의 자식 노드이다.
- slibing 관계: 같은 부모 아래의 노드들 끼리의 관계 - F, G 의 관계
- 조상 (Ancestor): 자식 노드 입장에서 부모의 부모 ... 로 올라가는 노드들 - H, I 입장에선 A, B, D 가 조상이다.
- 후손 (Descendant): 부모 노드 입장에서 자식의 자식 ... 로 내려가는 노드들 - A 입장에선 나머지노드들이 후손이다.
- 노드의 수준 (Level): 루트 노드로부터 해당 노드까지 도달했을 때 거치는 간선의 갯수로 정의한다. - 루트 노트: Level 0, 밑으로 내려가면서 level 이 1 씩 올라간다.
- 트리의 높이 (Height) = 최대 수준 (level) + 1,깊이 (depth) 라고도 한다 - 여기서의 높이는 4이다.
- 부분 트리 (서브트리 - Subtree): 트리에서 어느 한 노드를 기준으로 그 아래에 있는 것들을 새로운 트리로 보는 것 - D 를 기준으로 봤을 때 D, H, I 를 새로운 부분트리로 볼 수 있다.
- 노드의 차수 (Degree): 자식 (서브트리) 의 수 - degree: 0 인 것은 리프 노드이다.
- 각 노드는 자식 노드를 여러 개 가질 수 있지만, 부모 노드는 단 하나만을 가질 수 있다.

<br/>

### &#128204; 이진 트리 (Binary Tree)

모든 노드의 차수가 2 이하인 트리이다.

- 빈 트리 (empty tree)
- 루트 노드 + 왼쪽 서브트리 + 오른쪽 서브트리 (왼쪽과 오른쪽 서브트리 또한 이진트리이다.)

> &#128173; 재귀적으로 정의할 수 있다.

![](https://yn-e-si.com/assets/images/program_dev/tree_2.JPG){: .align-center}

<br/>

#### 포화 이진 트리 (Full Binary Tree)

모든 레벨에서 노드들이 모두 채워져 있는 이진 트리이다.

> &#128173; 리프 노드 들이 같은 높이에 있는 것이 특징이다.
>
> &#128173; 높이가 $k$ 이고, 노드의 개수가 $2^k -1$ 인 이진 트리이다.

![](https://yn-e-si.com/assets/images/program_dev/tree_2.JPG){: .align-center}

<br/>

#### 완전 이진 트리 (Complete Binary Tree)

리프 노드들이 왼쪽부터 채워지는 것이 특징이다. 높이가 $k$ 인 완전 이진트리는 level 이 $ k -2$ 까지는 모든 노드가 2 개의 자식을 가진 포화 이진 트리이고, level 이 $k-1$ 부터는 포화 이진 트리가 아니더라도 왼쪽부터 노드가 순차적으로 채워져 있는 이진 트리의 형태를 띄고 있다.

> &#128173; 트리를 이용한 검색에서는 완전 이진 트리에 가까울 수록 높은 성능을 내기에 데이터를 배치할 때는 최대한 완전 이진 트리의 모습과 가깝게 배치하는 것이 좋다.

![](https://yn-e-si.com/assets/images/program_dev/tree_3.JPG){: .align-center}

<br/>

#### 이진 트리의 추상적 자료구조

##### 연산의 정의

- <code>size()</code> - 현재 트리에 포함되어 있는 노드의 수를 구함
- <code>depth()</code> - 현재 트리의 깊이 (또는 높이; height) 를 구함
- <code>traversal()</code> - 정해진 순서대로 노드를 방문해서 처리하는 것

<br/>

##### 이진 트리의 구현 - 노드 (Node)

Node

- Data
- Left Child
- Right Child

```python
class Node:
	def __init__(self, item):
		self.data = item
		self.left = None
		self.right = None
```

<br/>

##### 이진 트리의 구현 - 트리 (Tree)

```python
# 이진 트리에서는 루트 노드만 주어지면 간선을 따라 내려가기에 루트 노드만 지정해 줌
class BinaryTree:
		def __init__(self, r):
			self.root = r
```

<br/>

##### 이진 트리의 구현 - <code>size()</code>

```python
# 재귀적인 방법으로 쉽게 구할 수 있음!
# 전체 이진 트리의 size() = left subtree 의 size() + right subtree 의 size() + 1 (자기 자신)

class Node:
	def size(self):
		l = self.left.size() if self.left else 0
		r = self.right.size() if self.right else 0
		return l + r + 1

class BinaryTree:
	def size(self):
		if self.root:
			return self.root.size()
		else: # empty tree 일 때
			return 0  
```

<br/>

##### 이진 트리의 구현 - <code>depth()</code>

```python
# 재귀적인 방법으로 쉽게 구할 수 있음!
# 전체 이진 트리의 depth() = left subtree 의 depth() 와 right subtree 의 depth() 중 더 큰 것 + 1

class Node:
		def depth(self):
			...

class BinaryTree:
		def depth(self):
			if self.root:
				return



class Node:

    def __init__(self, item):
        self.data = item
        self.left = None
        self.right = None


    def size(self):
        l = self.left.size() if self.left else 0
        r = self.right.size() if self.right else 0
        return l + r + 1


    def depth(self):
        l = self.left.depth() if self.left else 0
        r = self.right.depth() if self.right else 0
        return l + 1 if l >= r else r + 1


class BinaryTree:

    def __init__(self, r):
        self.root = r

    def size(self):
        if self.root:
            return self.root.size()
        else:
            return 0


    def depth(self):
        if self.root:
            return self.root.depth()
        else:
            return 0

```

<br/>

#### 이진 트리의 순회 (Traversal)

- 깊이 우선 순회 (Depth first traversal)
  - 중위 순회 (In - order traversal)
  - 전위 순회 (Pre - order traversal)
  - 후위 순회 (Post - order traversal)
- 너비 우선 순회 (Breadth first traversal)



##### 중위 순회 (In - order Traversal)

![](https://yn-e-si.com/assets/images/program_dev/tree_4.JPG){: .align-center}

순회 순서:

1. Left subtree
2. 자기 자신
3. Right subtree



왼쪽 하위트리부터 시작해서 루트를 거쳐 오른쪽 하위트리를 방문하는 순회이다.

위 그림에선 C, B, D 를 방문하여 왼쪽 하위트리를 거쳐 루트노드인 A를 방문, 이후에 오른쪽 하위트리 중 가장 왼쪽에 있는 F를 방문하고 이후 E, G 순서로 방문을 하게 된다.



```python
class Node:
	def inorder(self):
		traversal = [] # 리턴하려는 방문순서가 담길 리스트
		if self.left:
			traversal += self.left.inorder()
		traversal.append(self.data)
		if self.right:
			traversal += self.right.inorder()
		return traversal

class BinaryTree:
	def inorder(self):
		if self.root:
			return self.root.inorder()
		else:
			return []
		
```

<br/>

##### 전위 순회 (Pre - order Traversal)

![](https://yn-e-si.com/assets/images/program_dev/tree_5.JPG){: .align-center}

순회 순서:

1. 자기 자신
2. Left subtree
3. Right subtree

루트 노드부터 시작하여 왼쪽 하위트리, 오른쪽 하위트리를 순차적으로 방문하는 순회이다. 위 그림에선 루트 노드인 A 를 시작으로 B 를 방문하고 다시 B 의 왼쪽 하위트리인 C 를 방문하고 오른쪽 하위트리인 D를 방문하게 된다. 이 후에 순차적으로 E, F, G 를 방문한다.

```python
class Node:

    def __init__(self, item):
        self.data = item
        self.left = None
        self.right = None


    def inorder(self):
        traversal = []
        if self.left:
            traversal += self.left.inorder()
        traversal.append(self.data)
        if self.right:
            traversal += self.right.inorder()
        return traversal


    def preorder(self):
        traversal = []
        traversal.append(self.data)
        if self.left:
            traversal += self.left.preorder() # left child 가 있는 지 확인하려는 것
        if self.right:
            traversal += self.right.preorder() # right child 가 있는 지 확인하려는 것
        return traversal


class BinaryTree:

    def __init__(self, r):
        self.root = r


    def inorder(self):
        if self.root:
            return self.root.inorder()
        else:
            return []


    def preorder(self):
        return self.root.preorder() if self.root else []

```

<br/>

##### 후위 순회 (Post - order Traversal)

![](https://yn-e-si.com/assets/images/program_dev/tree_6.JPG){: .align-center}

순회 순서:

1. Left subtree
2. Right subtree
3. 자기 자신

왼쪽 하위트리부터 시작하여 오른쪽 하위트리를 방문하고 마지막으로 루트 노드를 방문하는 순회이다. 위 그림에선 왼쪽 하위트리인 C 를 제일 먼저 방문하고 C 에서의 오른쪽 하위트리인 D를 방문, 이후 B 를 방문한다.그리고 오른쪽 하위트리 중 제일 왼쪽 하위트리인 F 를 방문하고 순차적으로 G, E, A 를 방문하게 된다.

```python
class Node:

    def __init__(self, item):
        self.data = item
        self.left = None
        self.right = None


    def inorder(self):
        traversal = []
        if self.left:
            traversal += self.left.inorder()
        traversal.append(self.data)
        if self.right:
            traversal += self.right.inorder()
        return traversal


    def postorder(self):
        traversal = []
        if self.left:
            traversal += self.left.postorder()
        if self.right:
            traversal += self.right.postorder()
        traversal.append(self.data)
        return traversal


class BinaryTree:

    def __init__(self, r):
        self.root = r


    def inorder(self):
        if self.root:
            return self.root.inorder()
        else:
            return []


    def postorder(self):
        return self.root.postorder() if self.root else []
```

<br/>

##### 너비 우선 순회 (Breadth First Traversal)

![](https://yn-e-si.com/assets/images/program_dev/tree_7.JPG){: .align-center}

순회 순서:

1. level 이 낮은 노드를 우선으로 방문
2. 같은 level  의 노드들 사이에서는 왼쪽 노드에서 오른쪽 노드 순으로 방문

level 이 가장 낮은 루트 노드부터 시작하여 리프 노드까지 내려가는 순회하는 방식이다. 이 때, 같은 level 에서는 왼쪽에서 오른쪽 순으로 방문한다. 위 그림에선 루트 노드인 A 를 시작으로 다음 level 인 B, C 중 왼쪽부터 B, C 순으로 방문하고 이 후 순차적으로 D, E, F, G, H, I, J, K, L 을 방문한다.

> &#128173; 재귀적 방법이 적합하지 않고, 나중에 방문할 노드들을 순서대로 기록해 두어야하기 때문에 큐를 이용하는 것이 좋다.

<br/>

너비 우선 순회 알고리즘 설계

- 큐가 비어있다면 루트 노드를 큐에 삽입한다.
- 큐에서 꺼낸 후 해당 노드 방문한다.
- 해당 노드의 왼쪽 자식 노드가 있다면 큐에 삽입한다.
- 해당 노드의 오른쪽 자식 노드가 있다면 큐에 삽입한다.
- 다 확인했다면 큐에 있는 값을 빼낸다.
- 위와 같은 과정을 거친 후 큐가 비어있다면 종료한다.



<br/>

너비 우선 순회 알고리즘 구현

```python
class BinaryTree:
	def bft(self):
		

1. (초기화) traversal <- 빈 리스트, q <- 빈큐
2. 빈 트리가 아니면, root node를 큐에 추가 (enqueue)
3. q 가 비어 있지 않은 동안 진행
	3.1 node <- q 에서 원소를 추출 (dequeue)
	3.2 node 를 방문 (append)
	3.3 node 의 왼쪽, 오른쪽 자식 (있으면) 들을 q 에 추가
4. q가 빈 큐가 되면 모든 노드 방문 완료

class ArrayQueue:

    def __init__(self):
        self.data = []

    def size(self):
        return len(self.data)

    def isEmpty(self):
        return self.size() == 0

    def enqueue(self, item):
        self.data.append(item)

    def dequeue(self):
        return self.data.pop(0)

    def peek(self):
        return self.data[0]


class Node:

    def __init__(self, item):
        self.data = item
        self.left = None
        self.right = None


class BinaryTree:

    def __init__(self, r):
        self.root = r


    def bft(self):
        traversal = []
        Queue = ArrayQueue()
        if self.root:
            Queue.enqueue(self.root)

        while not Queue.isEmpty():
            q = Queue.dequeue()
            traversal.append(q.data)
            if q.left:
                Queue.enqueue(q.left)
            if q.right:
                Queue.enqueue(q.right)            
        return traversal
```

<br/>

<br/>

## &#128161; Check Point

- 트리에 관한 용어와 트리의 종류들에 대해 잘 숙지하기!
- 이진 트리의 순회 방식인 전위, 중위, 후위 순회와 너비 우선 순회의 구현에 대해 잘 숙지하기!