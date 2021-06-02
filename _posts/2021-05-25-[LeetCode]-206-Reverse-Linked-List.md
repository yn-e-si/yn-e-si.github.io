---
title: "[LeetCode] 206. Reverse Linked List "
excerpt: "파이썬 알고리즘 인터뷰"
toc: true
toc_sticky: true
use_math: true
categories:
 - CS
tags:
 - 파이썬알고리즘인터뷰
 - 자료구조
 - 알고리즘
 - 리트코드
 - 연결 리스트

---
## &#128161; 206. 역순 연결 리스트
[[문제 출처]](https://leetcode.com/problems/reverse-linked-list/)


### &#128204; 문제 설명
- 주어진 연결 리스트를 역순으로 리턴해야한다.

<br/>

### &#128204; 제한 사항

- The number of nodes in the list is the range [0, 5000]
- $-5000 \leq Node.val \leq 5000$

<br/>

### &#128204; 문제 분석
- 연결 리스트가 주어진다.
- 이를 역순으로 리턴하면 되므로 ``next`` 를 수정해주면 된다.

<br/>

### &#128204; 알고리즘 설계
- 이전의 ``next`` 를 담을 변수 ``prev`` 를 선언한다.
- ``node.next`` 를 ``prev`` 로 연결하면서 끝날때까지 반복한다.

<br/>

### &#128204; 코드 구현
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        node, prev = head, None
        
        while node:
            next, node.next = node.next, prev
            prev, node = node, next
        
        return prev

```

<br/>

### &#128204; 재귀 풀이
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        def reverse(node: ListNode, prev: ListNode = None):
            if not node:
                return prev
            next, node.next = node.next, prev
            return reverse(next, node)
        
        return reverse(head)
```
- ``next`` 와 ``node`` 를 파라미터로 지정함 함수를 계속해서 재귀 호출 한다.
- ``node`` 가 ``None`` 이 될 때까지 재귀호출하면 마지막에는 백트래킹되면서 연결 리스트가 거꾸로 연결된다.


<br/>
<br/>

## &#128161; Check Point
- while loop RunTime: 32 ms
- recursive RunTime: 40 ms
- 성능 차이는 두 개의 방식에서 큰 차이는 나지 않지만 재귀 구조의 특성 상 공간 복잡도가 좀 더 높게되므로 여기선 while loop 이 좀 더 효율적인 것 같다.
- 다만, 아직도 재귀로 푸는 방식은 익숙치가 않다...ㅠ