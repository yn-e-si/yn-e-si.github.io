---
title: "[Programmers Dev] 힙 (Heaps) "
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

## &#128161; 힙 (Heaps)

## &#128204; 힙( Heap) 이란?

이진 트리의 한 종류 (이진 힙 - binary heap)

- 루트 (root) 노드가 언제나 최댓값 또는 최솟값을 가진다.
  - 최대 힙 (max heap), 최소 힙 (min heap)

  > &#128173; 느슨한 정렬을 가지는 특징이 있다.

- 완전 이진 트리여야 한다.

- 재귀적으로도 정의된다.



#### 이진 탐색 트리와의 비교

- 원소들은 완전히 크기 순으로 정렬되어 있는가?

> &#128173; 이진 탐색 트리: O, 힙: X (느슨한 정렬)

- 특정 키 값을 가지는 원소를 빠르게 검색할 수 있는가?

> &#128173; 이진 탐색 트리: O, 힙: X

- 부가의 제약 조건은 어떤 것인가?

> &#128173; 힙: 완전 이진 트리여야한다는 조건이 있다.



#### 최대 힙 (Max Heap) 의 추상적 자료구조

연산의 정의

- <code>init()</code> - 빈 최대 힙을 생성
- <code>insert(item)</code> - 새로운 원소를 삽입
- <code>remove()</code> - 최대 원소 (root node) 를 반환 그리고 동시에 이 노드를 삭제



#### 데이터 표현의 설계

배열을 이용한 이진 트리의 표현

> &#128173; 완전 이진 트리이므로 시도하기가 좋다.

- 노드 번호 <code>m</code> 을 기준으로
  - 왼쪽 자식의 번호: $2*m$
  - 오른쪽 자식의 번호: $2*m + 1$
  - 부모 노드의 번호: $m//2$
- 완전 이진 트리이므로
  - 노드의 추가/삭제는 마지막 노드에서만 진행이 된다.

<br/>

#### 코드의 구현

<br/>

**빈 힙 생성**

```python
class MaxHeap:
    def __init__(self):
        self.data = [None]
```

<br/>

최대 힙에 원소 삽입

- 알고리즘 설계
  - 트리의 마지막 자리에 새로운 원소를 임시로 저장한다.
  - 부모 노드와 키 값을 비교하여 큰 값이라면 위로 이동시킨다.
- 복잡도
  - 원소의 개수가 $n$ 인 최대 힙에 새로운 원소를 삽입한다.
    - 부모 노드와의 대소 비교 최대 횟수: $log_2N$
    - 최악 복잡도 $O(log n)$ 의 삽입 연산
    - 최대 힙의 좋은 장점이다.

<br/>

**삽입 연산의 구현** - <code>insert(item)</code>

```python
class MaxHeap:
    def insert(self, item):
        # 힙의 마지막 자리에 값 추가
        self.data.append(item)
        
        # 배열로 선언되었으므로 idx 는 길이 - 1
        idx = len(self.data) - 1
        
        # 배열의 제일 앞 0 인덱스는 비워두고 제일 root node 는 인덱스가
        # 1 이므로 1 이 아닐 때 까지 루프를 돔
        while idx != 1:
            # 부모 노드와 키 값을 비교하여 값 변경
            if self.data[idx//2] < self.data[idx]:
                self.data[idx//2], self.data[idx] = self.data[idx], self.data[idx//2]
                idx = idx // 2
            else:
                break
```

<br/>

최대 힙에서 원소의 삭제 (최대 원소를 삭제)

- 알고리즘 설계

  - 루트 노드를 제거한다. (원소들 중 최댓값)
  - 트리 마지막 자리 노드를 임시로 루트 노드의 자리에 배치한다.

  > &#128173; 완전 이진 트리의 모양을 갖추기 위함이다.

  - 자식 노드들과의 값 비교를 하여 아래로, 아래로 이동한다.

  > &#128173; 자식이 둘 있을 경우, 둘 중에 더 큰 값을 기준으로 선택한다.

- 복잡도
  - 원소의 개수가 $n$ 인 최대 힙에서 최대 원소를 삭제한다.
    - 자식 노드들과의 대소 비교 최대 횟수: $2log_2N$
    - 최악 복잡도 $O(log n)$ 의 삭제 연산

<br/>

**삭제 연산의 구현** - <code>remove(), maxHeapify()</code>

```python
class MaxHeap:
	def remove(self):
        
		if len(self.data) > 1:
            
			# MaxHeap에서의 루트 노드와 트리 마지막 자리 노드를 교환
			self.data[1], self.data[-1] = self.data[-1], self.data[1]
            
            # MaxHeap 안에서의 최대 원소를 pop
			data = self.data.pop(-1) 
            
            # root node 부터 해서 MaxHeap의 구조를 유지하도록 하는 것 
			self.maxHeapify(1) 

		else:
			data = None
            
		return data



	def maxHeapify(self, i):
        # 왼쪽 자식 (left child) 의 인덱스를 계산합니다.
        left = 2 * i

        # 오른쪽 자식 (right child) 의 인덱스를 계산합니다.
        right = 2 * i + 1

        smallest = i
        # 왼쪽 자식이 존재하는지, 그리고 왼쪽 자식의 (키) 값이 (무엇보다?) 더 큰지를 판단합니다.
        if left < len(self.data) and self.data[left] > self.data[smallest]:
            # 조건이 만족하는 경우, smallest 는 왼쪽 자식의 인덱스를 가집니다.
            smallest = left

        # 오른쪽 자식이 존재하는지, 그리고 오른쪽 자식의 (키) 값이 (무엇보다?) 더 큰지를 판단합니다.
        if right < len(self.data) and self.data[right] > self.data[smallest]:
            # 조건이 만족하는 경우, smallest 는 오른쪽 자식의 인덱스를 가집니다.
            smallest = right

        if smallest != i:
            # 현재 노드 (인덱스 i) 와 최댓값 노드 (왼쪽 아니면 오른쪽 자식) 를 교체합니다.
            self.data[i], self.data[smallest] = self.data[smallest], self.data[i]

            # 재귀적 호출을 이용하여 최대 힙의 성질을 만족할 때까지 트리를 정리합니다.
            self.maxHeapify(smallest)
```

<br/>

#### 최대/최소 힙의 응용

- 우선 순위 큐 (priority queue)

  - Enqueue 할 때 "느슨한 정렬"을 이루고 있도록 한다 - $O(log n)$
  - Dequeue 할 때 최댓값을 순서대로 추출한다 - $O(logn)$
  - 양방향 연결 리스트 이용 구현과 효율성을 비교한다.

  > &#128173; 힙이 더 효율적이다.

- 힙 정렬 (heap sort)

  - 정렬되지 않은 원소들을 아무 순서로나 최대 힙에 삽입한다. - $O(logn)$
  - 삽입이 끝나면, 힙이 비게 될 때까지 하나씩 삭제한다 - $O(log n)$
  - 원소들이 삭제된 순서가 원소들의 정렬 순서이다.
  - 정렬 알고리즘의 복잡도 - $O(nlogn)$

<br/>

**힙 정렬 (heap sort) 의 코드 구현**

```python
def heapsort(unsorted):
	H = MaxHeap()
    
	for item in unsorted:
		H.insert(item)
        
	sorted = []
	d = H.remove()
    
	while d:
		sorted.append(d)
		d = H.remove()
        
	return sorted
```

<br/>

<br/>

## &#128161; Check Point

- 힙은 완전 이진 트리여야 한다는 제약이 있다.

- 루트 노드가 최댓값 혹은 최솟값이라는 특징이 있기에 이를 활용한 연산에서 효율적으로 사용될 수 있다.