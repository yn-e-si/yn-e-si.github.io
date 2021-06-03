---
title: "[LeetCode] 92. Reverse Linked List II "
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
## &#128161; 92. 역순 연결 리스트 II
[[문제 출처]](https://leetcode.com/problems/reverse-linked-list-ii/)

### &#128204; 문제 설명
- 연결 리스트와 시작을 가리키는 ``left``, 끝을 가리키는 ``right`` 변수가 주어진다.
- 연결 리스트 내에서 ``left`` ~ ``right`` 범위의 값을 역순으로 바꾸어 리턴해야한다.

<br/>

### &#128204; 제한 사항
- The number of nodes in the list is n.
- $1 \leq n \leq 500$
- $-500 \leq Node.val \leq 500$
- $1 \leq left \leq right \leq n$

<br/>

### &#128204; 문제 분석
- 역순이 시작되는 지점과 끝나는 지점이 주어진다.
- 연결 리스트 내에서 해당 지점에 속하는 구간을 역순으로 바꾸어 리턴해주면 된다.

<br/>

### &#128204; 알고리즘 설계
- 연결 리스트의 ``val`` 값을 담을 ``list`` 타입의 변수 ``L`` 을 선언한다.
- ``val`` 값을 담고 역순으로 바꾸어야하는 구간을 슬라이싱으로 변경하여 다시 연결 리스트로 변환한다.
<br/>

### &#128204; 코드 구현
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseBetween(self, head: ListNode, left: int, right: int) -> ListNode:
        if left == right:
            return head
        L: List = []
        root = node = ListNode(0)
        while head:
            L.append(head.val)
            head = head.next

        L[left -1: right] = L[right - len(L) - 1: -(len(L) - left + 2):-1]
        
        for i in L:
            node.next = ListNode(i)
            node = node.next
        
        return root.next

```

<br/>

### &#128204; 반복 구조로 노드 뒤집기
```python
def reverseBetween(self, head: ListNode, m: int, n: int) -> ListNode:
    # 예외 처리
    if not head or m == n:
        return head
    root = start = ListNode(None)
    root.next = head
    # start, end 지정
    for _ in range(m - 1):
        start = start.next
    end = start.next

    # 반복하면서 노드 차례대로 뒤집기
    for _ in range(n - m):
        tmp, start.next, end.next = start.next, end.next, end.next.next
        start.next.next = tmp
    return root.next
```
- ``start`` 는 변경이 필요한 ``left`` 의 바로 앞 지점을 가리키게 한다.
- ``end`` 는 ``start.next`` 인 ``left`` 를 가리키게 한다.
- ``start.next.next = tmp`` 는 이전에 ``start.next`` 였던 노드를 배치하는 것과 동일하다.
- 위와 같은 다중 할당을 ``right - left`` 만큼 반복하여 해당 구간의 값을 역순으로 배치한다.

<br/>
<br/>

## &#128161; Check Point
- 연결 리스트 문제에서 리스트로 변형하여 풀이하는 방식은 일종의 편법(?) 과도 같은 풀이이다.
- 바로 생각나는 풀이 방식으로 풀다보니 편법처럼 풀이를 해버린 것 같다.
- 연결 리스트에 좀 더 익숙해지기 위해 위와 같이 노드의 ``next``를 직접 변경해주어 동작하는 알고리즘 풀이를 숙지해두어야 할 것 같다.