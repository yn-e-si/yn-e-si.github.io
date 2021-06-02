---
title: "[LeetCode] 2. Add Two Numbers "
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
## &#128161; 2. 두 수의 덧셈
[[문제 출처]](https://leetcode.com/problems/add-two-numbers/)


### &#128204; 문제 설명
- 음수가 아닌 값들로 이루어진 연결 리스트 두 개가 주어진다.
- 각 값들은 역순으로써 합치면 정수 하나를 의미한다.
- 즉, [2, 3, 5] 일 경우 ``532`` 를 의미한다.
- 이럴 경우 두 개의 연결리스트의 합해진 값을 연결 리스트로 반환해야한다.

<br/>

### &#128204; 제한 사항

- The number of nodes in each linked list is in the range [1, 100].
- $0 \leq Node.val \leq 9$
- It is guaranteed that the list represents a number that does not have leading zeros.

<br/>

### &#128204; 문제 분석
- ``linked list`` 방식으로 접근하는 것이 아닌 야매? 스럽게 접근했다.
- 숫자의 합을 구해야하므로 자릿수의 영향을 받지 않기위해 ``str`` 로 값을 변환해준뒤 다시 ``int`` 타입으로 변환해서 사용한다.

<br/>

### &#128204; 알고리즘 설계
- 두 개의 연결 리스트의 ``val`` 값을 담을 두 변수를 선언한다.
- 각 ``while`` 문을 돌면서 ``val`` 값을 담는다.
- 두 변수를 하나의 ``list`` 로 만들고 다시 ``linked list`` 로 변환한다.

<br/>

### &#128204; 코드 구현
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        root = node= ListNode(0)
        L1: str = ''
        L2: str = ''
        while l1:
            L1 += str(l1.val)
            l1 = l1.next
        while l2:
            L2 += str(l2.val)
            l2 = l2.next
        for i in list(map(int,str(int(L1[::-1]) + int(L2[::-1]))))[::-1]:
            node.next = ListNode(i)
            node = node.next
        return root.next
```

<br/>

### &#128204; 자료형 변환 풀이
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    # 연결 리스트 뒤집기
    def reverseList(self, head: ListNode) -> ListNode:
        node, prev = head, None

        while node:
            next, node.next = node.next, prev
            prev, node = node, next

        return prev

    # 연결 리스트를 파이썬 리스트로 변환
    def toList(self, node: ListNode) -> List:
        list: List = []
        while node:
            list.append(node.val)
            node = node.next
        return list

    # 파이썬 리스트를 연결리스트로 변환
    def toReversedLinkedList(self, result: str) -> ListNode:
        prev: ListNode = None
        for r in result:
            node = ListNode(r)
            node.next = prev
            prev = node
        
        return node

    # 두 연결 리스트의 덧셈
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        a = self.toList(self.reverseList(l1))
        b = self.toList(self.reverseList(l2))

        resultStr = int(''.join(str(e) for e in a)) + \
                    int(''.join(str(e) for e in b))

        # 최종 계산 결과 연결 리스트 변환
        return self.toReversedLinkedList(str(resultStr))
```
- ``int(''.join(str(e) for e in a))`` 코드 부분을 다음과 같이 보다 간략하게 변경이 가능하다.
- ``int(''.join(map(str, a)))``
- ``functools.reduce(lambda x, y: 10 * x + y, a, 0)``
-  ``functools``: 함수를 다루는 함수를 뜻하는 고계 함수를 지원하는 함수형 언어 모듈이다.
-  ``reduce``: 두 인수의 함수를 누적 적용하라는 메소드이다.
-  따라서 위 코드의 작동은 ``x`` 에 계속 10 을 곱하면서 자릿수 ($10^n$) 형태로 올려나가고 그 뒤에 ``y`` 를 더해서 $10^0$ 자릿수를 채워나가는 방식이다.

<br/>

### &#128204; 전가산기 풀이
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        root = head = ListNode(0)

        carry = 0
        while l1 or l2 or carry:
            sum = 0
            # 두 입력값의 합 계산
            if l1:
                sum += l1.val
                l1 = l1.next
            if l2:
                sum += l2.val
                l2 = l2.next

        # 몫(자리올림수) 과 나머지(값) 계산
        carry, val = divmod(sum + carry, 10)
        head.next = ListNode(val)
        head = head.next

    return root.next

```
- ``carry, val = divmod(sum + carry, 10)``: 가산 결과가 두 자릿수가 될 경우 몫은 자리올림수로 설정해 다음번 연산에 사용되게 하고 나머지는 값으로 취한다.




<br/>
<br/>

## &#128161; Check Point
- 전가산기 방식이라는 것을 처음 알게되었다.
- 자릿수가 넘어가는 것을 표현하기 위해 조금 더 복잡한 방식만 떠올렸었는데 위이 방식을 보니 코드의 가독성과 간결성에서 큰 장점이 있는 것 같다.
- 숫자형 리스트를 단일값으로 변환할 때, ``join`` 과 ``map`` 정도의 코드만 알고있었는데 ``functools.reduce`` 라는 새로운 모듈의 사용법을 알게되었다.