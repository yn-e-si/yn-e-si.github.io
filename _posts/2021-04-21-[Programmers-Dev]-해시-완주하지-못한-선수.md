---
title: "[Programmers Dev] lv1_완주하지 못한 선수 "
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

## &#128161; lv1_완주하지 못한 선수

[[문제 출처]](https://programmers.co.kr/learn/courses/30/lessons/42576)

### &#128204; 문제 설명

- 수많은 마라톤 선수들이 마라톤에 참여하였습니다. 
- 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다. 
- 마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요. 

### &#128204; 제한 사항

- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다. 
- completion의 길이는 participant의 길이보다 1 작습니다. 
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다. 
- 참가자 중에는 동명이인이 있을 수 있습니다.

### &#128204; 문제 분석

- $1 \leq participant \leq 100,000$ 의 범위를 보면 시간복잡도가 $O(n)$ 또는 $O(logn)$ 이 가능할 것이라는 것을 예상할 수 있다.
- 동명이인이 없다면 set 을 통해 차집합을 구현하면 되지만 동명이인이 있으므로 사용할 수 없다.
- 이름이 주어지면 배열에 몇 번 등장했는지 알아야하므로 이름의 등장횟수를 기록해야 한다.
- 이름 대신 번호가 주어졌다면 list 를 사용할만 하지만 문자열로 주어지기에 이는 list 에 담기는 부담스럽다. 따라서, hash 자료구조인 dict 를 통해 접근을 한다.

### &#128204; 알고리즘 설계

- <code>.get(x, 0)</code> 을 통해 dict 에 이름의 등장횟수를 해시로 저장한다.
- 이 후, for loop 을 돌면서 완주한 사람의 횟수를 제거한다.
- 만약, 완주하지 못했다면 dict 에 값이 존재 하기에 이를 리턴한다.



### &#128204; 코드 구현

```python
def solution(participant, completion):
	d = {}
	for x in participant:
		d[x] = d.get(x, 0) + 1 # 처음 나온 것은 +1 , 기존에 있던 것은 기존 횟수 + 1
	for x in completion:
		d[x] -= 1  # completion 에 있는 횟수 만큼 -1 씩 감소
	dnf = [k for k, v in d.items() if v > 0] # 완주하지 못한 사람의 key 값을 담음
	answer = dnf[0] 
	return answer

3~4에 있는 for 문은 dict에 update하는 것이기 때문에 
participant 라는 배열의 길이에 비례

5~6도 위와 마찬가지로 길이에 비례하는 복잡도를 가짐


dnf 를 정의하는 것은 d라는 사전에 들어있는 모든 원소를 나열하고 if 조건을 만족하는
경우에 리스트로 만드는 연산이기에 사전에 들어있는 모든 원소를 꺼내기에
사전의 크기에 비례하는 복잡도를 가짐

결국, 시간복잡도는 participant의 길이에 비례하는 선형 복잡도를 가짐

이를 만들 수 있던 것은 해시 테이블을 상수시간에 읽고쓸수있었기 때문에 가능했던 것

핵심은 해시구조를 사용할 수 있느냐 라는 것
```

- for loop 이 두 개가 사용되었기에 $O(n^2)$ 의 복잡도를 가진다고 생각할 수 있지만, 첫 번째 for loop 은 dict 에 update 하는 것이기에 participant 의 길이에 비례한다.
- 리스트 컴프리헨션을 사용한 부분은 dict 의 크기에 비례하는 복잡도를 가진다.
- 따라서, 시간복잡도는 participant 의 길이에 비례하는 선형 복잡도 $O(n)$ 를 가진다.



### &#128204; 정렬을 이용한 코드

```python
def solution(participant, completion):
	participant.sort()
	completion.sort()
	for i in range(len(completion)):
		if participant[i] != completion[i]:
			return participant[i]
	return participant[len(participant)-1]


최저: O(NlogN) 

```

- 정렬의 시간복잡도는 $O(NlogN)$ 을 가진다.
- 이는 위에 해시를 사용한 시간복잡도 보다 크다.

## &#128161; Check Point

- 문자열 같은 경우, 확실히 list 를 사용하는 것보다 dict 가 연산에 있어 유리한 것 같다.
- 이 문제같은 경우, 정렬을 이용한 알고리즘보다 dict 를 이용한 알고리즘이 복잡도에 있어 유리한 측면을 가졌다. 그렇다고 항상 dict 가 유리하다라고는 할 수 없지만 역시 여러 방향으로 연습을 해보는게 좋을 것 같다.