---
title: "[LeetCode] 234. Palindrome Linked List"
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
 - 문자열

---
## &#128161; 234. 팰린드롬 연결 리스트


### &#128204; 문제 설명
- 주어진 연결 리스트가 팰린드롬 구조인지 판별해야한다.

<br/>

### &#128204; 제한 사항
- The number of nodes in the list is in the range $[1, 10^5]$
- $0 \leq Node.val \leq 9$

<br/>

### &#128204; 문제 분석
- 주어진 매개변수 <code>head</code> 는 연결 리스트 이므로 이를 <code>list</code> 혹은 <code>deque</code> 로 변경해서 팰린드롬 구조인지 판별하면 될 것 같다.

<br/>

### &#128204; 알고리즘 설계
- 우선 주어진 연결 리스트 <code>head</code> 를 <code>pop</code> 연산에서 <code>list</code>보다 최적화된 구조인 <code>deque</code> 구조로 바꿔준다.
- <code>popleft</code> 와 <code>pop</code> 을 이용해서 팰린드롬 구조인지 판별한다.
<br/>

### &#128204; 코드 구현

**Deque 사용**
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        if head is None:
            return False

        l = collections.deque()

        node = head

        while node is not None:
            l.append(node.val)
            node = node.next
            
        for _ in range(len(l)//2):
            left = l.popleft()
            right = l.pop()
            if left != right:
                return False
        else:
            return True

```
- <code>list</code> 가 아닌 <code>deque</code> 구조 이므로 <code>popleft</code> 를 사용해서 <code>list</code> 보다 효율적으로 <code>pop</code> 연산기 가능하다.
- Runtime: 984 ms

<br/>

**List 사용**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        l: List = []
        if not head:
            return True
            
        node = head
        while node is not None:
            l.append(node.val)
            node = node.next
            
        while len(l) >1:
            if l.pop(0) != l.pop():
                return False

        return True
```
- <code>deque</code> 가 아닌 <code>list</code> 로 구현한 코드이다.
- 효율성의 측면에서 보면 확실히 <code>deque</code> 와 차이가 남을 알 수가 있다.
- Runtime: 2192 ms

<br/>

**파이써닉한 방식**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        l = []
        node = head

        while node is not None:
            l.append(node.val)
            node = node.next   
               
        return l == l[::-1]
```
- 이와 같이 파이써닉하게 <code>list</code> 를 뒤집어서 확인할 수도 있다.
- 효율성에서 <code>deque</code> 와 큰 차이가 나진 않았다.
- Runtime: 948 ms
<br/>

### &#128204; 모범 풀이 - 런너를 이용한 풀이
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
       rev = None
       slow = fast = head

       # 런너를 이용해 역순 연결 리스트 구성
       while fast and fast.next:
           fast = fast.next.next
           rev, rev.next, slow = slow, rev, slow.next
        # 주어진 연결 리스트가 홀 수일 경우 중간의 값을 피하기 위한 코드
        if fast:
            slow = slow.next

        # 팰린드롬 여부 확인
        while rev and rev.val == slow.val:
            slow, rev = slow.next, rev.next
        return not rev

```
- 런너 풀이의 핵심은 <code>fast</code> 와 <code>slow</code> 의 두 변수를 사용하여 비교 시점을 정하는 것이다.
- <code>fast</code> 같은 경우 <code>slow</code> 보다 2배 빠른 속도로 이동하게 되는데 이는 <code>fast</code> 가 끝에 도달할 때 <code>slow</code> 는 중간에 위치하게 된다.
- 이때 <code>slow</code> 가 중간 위치할 때까지의 값들을 역순으로 연결리스트를 만든다.
- 이 후, 중간부터 남은 끝까지의 값들과 비교했을 때 값들이 일치한다면 이는 팰린드롬이라고 판단할 수 있다.
- 팰린드롬일 경우 마지막 <code>while loop</code> 을 통해 None 값이 나오게 된다.



<br/>
<br/>

## &#128161; Check Point
- 동적 배열로 구성된 <code>list</code> 는 첫 번째 값을 꺼내오면 모든 값이 한 칸씩 시프팅되기 때문에 시간 복잡도가 $O(n)$ 이 걸린다.
- 따라서 최적화를 위해서 이중 연결 리스트 구조로 되어 있는<code>deque</code> 구조가 사용해야 한다.
- <code>deque</code> 구조 같은 경우 양쪽 방향 모두 추출하는데 시간 복잡도가 $O(1)$ 이 걸린다.
- 런너풀이라는 색다른 풀이법을 알게되었다. 이 기법같은 경우에는 연결 리스트 문제에서 자주 쓰이게 되는 기법이라 한다. 투 포인터처럼 비교하거나 뒤집기 등 여러 상황에서 단일 변수보다 여러 변수를 통해 접근을 하며 효율을 높이는 기법이 많이 존재하는 것 같다. 이러한 기법들을 충분히 학습하고 흡수해야할 것 같다.