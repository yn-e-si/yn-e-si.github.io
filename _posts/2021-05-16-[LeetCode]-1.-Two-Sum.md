---
title: "[LeetCode] 1. Two Sum "
excerpt: "파이썬 알고리즘 인터뷰"
toc: true
toc_sticky: true
categories:
 - CS
tags:
 - 파이썬알고리즘인터뷰
 - 자료구조
 - 알고리즘
 - 리트코드
 - 문자열
use_math: true
---

## &#128161; 1. 두 수의 합

### &#128204; 문제 설명

- 주어진 리스트 <code>nums</code> 에 있는 값 중 두 수를 더했을 때, <code>target</code> 이 되는 <code>index</code> 를 반환해야한다. 

### &#128204; 제한 사항

- $2 \leq nums.length \leq 10^3$
- $-10^9 \leq nums[i] \leq 10^9$
- $-10^9 \leq target \leq 10^9$



### &#128204;문제 분석

- 주어진 리스트의 값 중에서 더했을 때 <code>target</code> 이 되는 두 수를 구하면 된다. 

### &#128204; 알고리즘 설계

- 단순하게 이중 for loop 을 돌면서 더했을 때 <code>target</code> 이 되는 두 수의 인덱스를 반환한다.

### &#128204; 코드 구현

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for n1 in range(len(nums)):
            for n2 in range(n1+1,len(nums)):
                if nums[n1] + nums[n2] == target:
                    return [n1,n2]
```

- 모든 값을 다 확인해보는 탐욕적 알고리즘이다.
- 시간복잡도는 $O(n^2)$ 이다.

### &#128204; 모범 풀이 - in 을 이용한 탐색

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i, n in enumerate(nums):
            complement = target -n
            
            if complement in nums[i + 1:]:
                return [nums.index(n), nums[i+1:].index(complement) + (i + 1)]
```

- <code>target</code> 에서 <code>n</code> 을 뺀 값이 남은 <code>nums</code> 에 있는지 <code>in</code> 을 통해 확인하는 방식이다.
- <code>in</code> 의 시간복잡도는 $O(n)$ 이므로 전체 시간복잡도는 $O(n^2)$ 이다.
- 하지만 <code>in</code> 은 파이썬에서 매번 값을 비교하는 것에 비해 훨씬 더 빨리 실행된다하니 위에 있는 내 풀이보다 더 빠르게 작동하는 것 같다.

### &#128204; 모범 풀이 - 첫 번째 수를 뺀 결과 키 조회

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        
        # 키와 값을 바꿔서 딕셔너리로 저장
        nums_map = { num: i for i, num in enumerate(nums)}
            
        # 타겟에서 첫 번째 수를 뺀 결과를 키로 조회
        for i, num in enumerate(nums):
            if target - num in nums_map and i != nums_map[target - num]:
                return [i, nums_map[target - num]]

```

- 두 번째 수를 키로하고 기존의 인덱스는 값으로 바꿔서 딕셔너리로 저장한다.
- 두 번째 수를 키로 조회하면 인덱스를 바로 구할 수가 있다.
- 딕셔너리의 조회는 평균적으로 $O(1)$ 에 접근 가능하므로 전체적인 시간복잡도는 $O(n)$ 이 된다.

### &#128204; 모범 풀이 - 조회 구조 개선

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        nums_map = {}
        # 하나의 for 문으로 통합
        for i, num in enumerate(nums):
            if target - num in nums_map:
                return [nums_map[target - num], i]
            nums_map[num] = i
```

- 바로 위의 코드와 비교했을 때 성능이 큰 차이가 나지는 않지만 코드가 보다 간결해졌다.

### &#128204; 모범 풀이 - 투 포인터 이용

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        left, right = 0, len(nums) - 1
        while not left == right:
            # 합이 타겟보다 작으면 왼쪽 포인터를 오른쪽으로
            if nums[left] + nums[right] < target:
                left += 1
            # 합이 타겟보다 크면 오른쪽 포인터를 왼쪽으로
            elif nums[left] + nums[right] > target:
                right -= 1
            else:
                return [left, right]
```

- 투 포인터를 사용한다면 코드가 보다 간결하고 이해하기가 쉽다.
- 시간복잡도는 $O(n)$ 이다.
- 하지만 투 포인터는 정렬된 상태에서만 사용이 가능하기에 이 문제에서는 적용이 불가능하다.
- 이 문제에서 사용할 경우 정렬을 한 후에 사용되기 때문에 인덱스가 꼬이게되는 문제가 생긴다.
- 만약 인덱스가 아니라 값을 찾아내는 문제라면 충분히 가능하지만 인덱스를 물어보는 문제이기에 사용이 불가능하다.



## &#128161; Check Point

- 아직 알고리즘을 생각할 때 습관적으로 for loop 을 너무 많이 쓰게 되는 것 같다.
- 충분히 파이써닉 하게 생각하다보면 for loop을 많이 안써도 될 텐데,,,계속해서 여러 문제와 코드방식을 접하면서 사고력을 넓혀가야 할 것 같다.