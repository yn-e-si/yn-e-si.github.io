---
title: "[LeetCode] 121. Best Time to Buy and Sell Stock "
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
## &#128161; 121. 주식을 사고팔기 가장 좋은 시점


### &#128204; 문제 설명
- 한 번의 거래로 낼 수 있는 최대 이익을 산출하라.

<br/>

### &#128204; 제한 사항

- $1 \leq prices.length \leq 105$
- $0 \leq prices[i] \leq 104$

<br/>

### &#128204; 문제 분석
- 각 인덱스는 날짜를 의미한다.
- 즉, 순서가 정해져있는 <code>list</code>이다.
- 저점과 고점을 조정해가며 값을 계산해야할 것 같다.
<br/>

### &#128204; 알고리즘 설계
- 최소값을 가장크게 설정해준다.
- for 문을 돌면서 저점과 비교해 더 작은 저점을 새로운 저점으로 지정한다.
- 이 후 해당 저점과 현재 값과의 차이를 계산하고 그 값이 기존 값보다 크다면 최대치로 값을 변경한다.

<br/>

### &#128204; 코드 구현
```python
def maxProfit(self, prices: List[int]) -> int:
    answer = 0
    min_num = sys.maxsize

    for price in prices:
        min_num = min(min_num, price)
        answer = max(answer, price - min_num)
    return answer
```

<br/>
<br/>

## &#128161; Check Point
- <code>min, max</code> 을 초기화 시켜 줄 때 임의의 큰 값이나 작은 값으로 초기화 시켜주는 것보단 <code>-sys.maxsize, sys.maxsize</code> 와 같이 초기화 시켜주는 것이 가장 안전한 방법인 것 같다.