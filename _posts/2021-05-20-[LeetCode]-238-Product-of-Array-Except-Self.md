---
title: "[LeetCode] 238. Product of Array Except Self "
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
 - 배열

---
## &#128161; 238. 자신을 제외한 배열의 곱
[[문제 출처]](https://leetcode.com/problems/product-of-array-except-self/)

### &#128204; 문제 설명
- 배열을 입력받아 <code>output[i]</code> 가 자신을 제외한 나머지 모든 요소의 곱셈 결과가 되도록 출력하라.


<br/>

### &#128204; 제한 사항
- 나눗셈을 사용하면 안된다.
- 시간복잡도를 $O(n)$ 안에 풀이해야 한다.

<br/>

### &#128204; 문제 분석
- 제한 사항만 없다면 쉽게 풀이가 가능하겠지만 제한 사항 때문에 풀이가 바로 떠오르진 않는 것 같다.
- for loop 을 총 2 번을 사용하여 한 번은 왼쪽에서 오른쪽 값을 곱해가며 나아가고 그 값을 오른쪽에서 왼쪽으로 한 번 더 곱한 값으로 구한다.

<br/>

### &#128204; 알고리즘 설계
- 곱셈이므로 처음 초기화를 0 이 아닌 1 로 시작한다.
- 처음 for loop 을 돌며 왼쪽에서 오른쪽 방향으로 값을 곱해 나간다.
- 이 후 두 번째 for loop 에선 처음 for loop 에서 얻은 <code>answer</code> 에서 오른쪽에서 왼쪽 방향으로 값을 곱해 나간다.

<br/>

### &#128204; 코드 구현

```python
def productExceptSelf(nums: List[int]) -> List[int]:
    multiply_num = 1
    answer = []

    for i in range(0,len(nums)):
        answer.append(multiply_num)
        multiply_num *= nums[i]
    
    multiply_num = 1
    for i in range(len(nums) - 1, -1, -1):
        answer[i] *= multiply_num
        multiply_num *= nums[i]

    return answer
```

<br/>
<br/>

## &#128161; Check Point
- 아이디어가 바로 떠오르지 않았던 문제이다.
- 또한 아이디어를 떠올렸을 때 바로 코드로 구현하는 것에 어려움을 느꼈다.
- 가장 어려움을 느꼈던 부분은 값을 초기화 시켜주는 부분과 범위 설정이였던 것 같다.
- 반복문의 처음과 끝을 항상 잘 생각하고 구현을 해야할 것 같다.
