---
title: "[LeetCode] 21. Merge Two Sorted Lists "
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
## &#128161; 21. 두 정렬 리스트의 병합
[[문제 출처]](https://leetcode.com/problems/merge-two-sorted-lists/)

### &#128204; 문제 설명
- 두 개의 linked lists 가 주어집니다.
- 두 linked lists 는 sorted 된 상태이고 이를 순서대로 merge 시켜서 하나의 linked lists 로 리턴하면됩니다.

<br/> 


### &#128204; 제한 사항
- The number of nodes in both lists is in the range [0, 50].
- $-100 \leq Node.val \leq 100$
- Both l1 and l2 are sorted in non-decreasing order.

<br/>

### &#128204; 문제 분석
- 주어진 linked lists 들이 정렬된 상태로 주어진다.
- 따라서, 앞에서부터 차례로 비교해 가며 리턴하면 된다.

<br/>

### &#128204; 알고리즘 설계
- l1과 l2 의 값을 비교해 작은 값이 왼쪽에 오게 swap 해준다.
- next 는 그 다음 값이 엮이도록 재귀 호출한다.

<br/>

### &#128204; 코드 구현
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:

        if not(l1) or (l2 and l1.val > l2.val):
            l1, l2 = l2, l1
        if l1:
            l1.next = self.mergeTwoLists(l1.next, l2)
        return l1
        

```

<br/>
<br/>

## &#128161; Check Point
- linked list 에서 재귀 호출을 사용하기에 구현에 있어 헷갈린 부분이 있었다.
- 실제 메모하면서 풀어나가는 것이 확실히 도움되는 것 같다.
- 파이썬에서의 다중 할당의 동작과정을 잊지말자!