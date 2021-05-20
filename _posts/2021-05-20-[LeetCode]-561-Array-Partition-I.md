---
title: "[LeetCode] 561. Array Partition I "
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
## &#128161; 561. 배열 파티션 I
### &#128204; 문제 설명
- <code>n</code> 개의 페어를 이용한 <code>min(a, b)</code> 의 합으로 만들 수 있는 가장 큰 수를 출력하라.

<br/>

### &#128204; 제한 사항
- $1 \leq n \leq 10^4$
- $nums.length == 2 * n$
- $-10^4 \leq nums[i] \leq 10^4$

<br/>

### &#128204; 문제 분석
- 항상 2 개의 pair 를 가지므로 작은 것은 작은 것끼리 큰 것은 큰 것끼리 묶어 <code>min</code> 을 진행했을 때 최대한 값의 손실을 적게 만들어야 한다.

<br/>

### &#128204; 알고리즘 설계
- 계산을 쉽게하기 위해 우선 정렬을 시킨다.
- 2 개의 pair 를 가지며 항상 길이가 $2*n$ 이므로 for loop 을 길이의 반만 loop 할 수 있게 설정한다.
- 이 후, pair 를 이룬 두 개의 값 중 작은 값만을 더해가며 최종 <code>answer</code> 를 반환한다.

<br/>

### &#128204; 코드 구현
```python
class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        nums.sort()
        answer = 0
        for i in range(0,len(nums)-1,2):
            answer += min(nums[i],nums[i+1])
        return answer
```
<br/>

### &#128204; 모범 풀이 - 파이썬다운 방식
```python
class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        return sum(sorted(nums)[::2])
```
- 파이써닉한 코드로 작성하면 위와 같이 한 줄로 작성이 가능하다.

<br/>
<br/>

## &#128161; Check Point
- 위의 두 코드는 성능상 차이는 없지만 파이써닉하게 짜게되면 코드가 간결해지는 특징이 있는 것 같다.
- 가독성이 떨어질정도로 파이써닉하게 짜는건 지양해야하겠지만 위와 같이 가독성의 문제가 없다면 파이써닉하게 짜는 연습도 자주 해봐야 할 것 같다.