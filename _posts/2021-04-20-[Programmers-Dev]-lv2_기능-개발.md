---
title: "[Programmers Dev] lv2_기능 개발 "
excerpt: "어서와! 자료구조와 알고리즘은 처음이지?"
toc: true
toc_sticky: true
categories:
 - CS
tags:
 - 프로그래머스
 - 자료구조
 - 알고리즘
 - 문제풀이
use_math: true
---

## &#128161; lv2_기능 개발

[[문제 출처]](https://school.programmers.co.kr/courses/11947/lessons/76990)

### &#128204; 문제 분석

- 먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses 와 각 작업의 개발 속도가 적힌 정수 배열 speeds 가 주어진다.
- 배포는 순서대로 이루어져야 하며, 하루에 한 번만 가능하다.
- 즉 3,4 번 째의 배포가 100% 가 되었어도 1,2 번이 100% 이 되지 않았다면 배포가 되지 않는다.
- 배포가 될 때, 몇 개의 기능이 배포되는지를 리턴한다.

### &#128204; 알고리즘 설계

- progresses 를 배포가 될 때까지 걸리는 일수로 새로 만든다.
- while loop 을 돌면서 index 가 가리키는 progresses 값이 0보다 작아질 때를 찾는다.
- 0보다 작거나 같아진다면 배포될 준비가 끝난 것이므로 cnt 를 +1 해준다. 이 때, 순서대로 배포되어야하므로 다음 인덱스가 0보다 작거나 같지 않다면 배포할 수 없는 것이므로 break 문으로 for loop 을 끝내준다.
- 만약 index 가 가리키는 progresses 값이 배포가 되었다면 cnt 는 가능한 수 만큼 증가했기에 해당 값을 answer list 에 추가하고 idx 는 그 수만큼 증가시켜서 중복계산을 막는다.
- 이 후 값이 다 적혀있는 answer list를 리턴해준다.

### &#128204; 코드 구현

```python
import math
def solution(progresses, speeds):   
    answer = []
    progresses = [ math.ceil((100 - p) / s) for p,s in zip(progresses, speeds)]
    
    idx, cnt = 0, 0
    
    while idx < len(progresses):
        temp = progresses[idx]
        
        for i in range(idx,len(progresses)):
            progresses[i] -= temp
            
        for i in range(idx,len(progresses)):
            if progresses[i] <= 0:
                cnt += 1
            else: break
                
        if cnt != 0:
            answer.append(cnt)
            idx += cnt
            cnt = 0
            
    return answer
```



### &#128204; 다른 사람 코드

```python
from math import ceil

def solution(progresses, speeds):
    answer = []
    max_duration = ceil((100 - progresses[0]) / speeds[0])
    count = 0
    
    for progress, speed in zip(progresses, speeds):
        duration = ceil((100 - progress) / speed)

        if max_duration < duration:
            answer.append(count)
            count = 0
            max_duration = duration
        count += 1
    
    if count > 0:
        answer.append(count)
    
    return answer
```

- 나의 풀이와 비슷하지만 복잡도면에서 위의 코드가 훨씬 효율적이다.
- 우선순위가 높은 제일 첫 인덱스가 배포에 걸리는 일 수를 max_duration 에 담는다.
- 이 후, for loop 을 돌면서 해당 duration 이 max_duration 보다 작을 경우는 뒤의 배포일이 더 빠르다는 것이므로 count + 1 를 해준다.
- duration 이 max_duration 보다 클 경우는 앞에 있는 배포일수가 충족한 것이므로 answer 의 그동안의 count 를 append 해주고 amx_duration 을 새로 조정해준다.
- 마지막 if 문은 for loop 이 끝나고 마지막 값의 배포를 추가해주기 위한 조건이다.
- for loop 이 한 번만 사용되므로 시간복잡도는 $O(n)$ 을 갖는다.





## &#128161; Check Point

- 내 코드에서는 하나의 for loop 에 작동하도록 다 넣어봤지만 배포가 순서대로 이루어져야 한다는 점, 앞의 배포가 끝나야 뒤에 배포가 가능하다는 점에서 이를 구현하기 위해 for loop 을 2개로 나누었다.
- 다른 코드를 보면, 기본적인 알고리즘은 비슷한지만 좀 더 효율적으로 계산함을 알 수 있었다.
- 모든 list 의 값을 새로 update 해 나가는 것이 아니라 계산에 필요한 값만을 따로 담고 이를 활용해서 계산하면서 시간복잡도가 훨씬 줄어듬을 알 수 있었다.
- 아직 이러한 구조에 대해 익숙치 않다보니 계속 연습해가면서 시간복잡도를 줄이도록 노력해야겠다.