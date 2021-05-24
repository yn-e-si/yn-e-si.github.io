---
title: "[Programmers Dev] Lv2. 큰 수 만들기  "
excerpt: "어서와! 자료구조와 알고리즘은 처음이지?"
toc: true
toc_sticky: true
use_math: true
categories:
 - CS
tags:
 - 프로그래머스
 - 자료구조
 - 알고리즘
 - 문제풀이

---
## &#128161; 
[[문제 출처]](https://programmers.co.kr/learn/courses/30/lessons/42883)

### &#128204; 문제 설명

- 어떤 숫자에서 k 개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.
- 예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.
- 문자열 형식으로 숫자 <code>number</code> 와 제거할 수의 개수 <code>k</code> 가 매개변수로 주어집니다. <code>number</code>에서 <code>k</code> 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

<br/>

### &#128204; 제한 사항
- $1 \leq number.length \leq 1000000$
- $1 \leq k \leq 10^{len(number) - k}$

<br/>

### &#128204; 문제 분석
- 앞 자리에서부터 하나씩 골라서 담되, 지금 담으려는 것보다 작은 것들은 뺀다.
- 단, 뺄 수 있는 수효에 도달할 때까지만 진행한다.

<br/>

### &#128204; 알고리즘 설계
- 주어진 숫자 <code>number</code> 로부터 하나씩 꺼내어 모으되 이미 모아둔 것 중 지금 등장한 것보다 작은 것들을 빼낸다.
- 이렇게 모은 숫자들을 자릿수 맞추어 반환한다.

<br/>

### &#128204; 코드 구현

```python
def solution(number, k):
	collected = []
	for i, num in enumerate(number):

		while len(collected) > 0 and collected[-1] < num and k > 0: # k > 0 : 뺴낼 개수가 남아있는 경우, collected[-1] : 마지막 글자가 현재 글자보다 작을 경우를 지칭
			collected.pop()
			k -= 1
		if k == 0: # if 문이 없더라도 정상적인 답이 도출되지만, 경우에 따라서는 이것이 더 효율적으로 동작할 수도 있음.
			collected += list(number[i:])
			break
		collected.append(num)
	collected = collected[: -k] if k >0 else collected # 아직까지 빼낼 경우가 남아있을 때만 동작
	answer = ''.join(collected)
	return answer
```
- <code>collected</code> - 하나하나씩 숫자를 모아서 큰 숫자를 만드는 것이 목적이다.
- <code>for loop</code>에서의 복잡도는 <code>number</code> 의 길이와 비례한다. 또한 이 안에 <code>while</code> 이 있으므로 이중 순환문이 된다. 
- 이중 순환문이기에 복잡도가 $O(\frac {n^2} {2})$  라고 생각할 수 있지만, <code>number</code> 라는 글자에서 한 글자씩 뽑았을 때 <code>collected</code>에 추가되는 것도 1번 나오는 것도 1번 이기에 전체 <code>for</code> 문으로 구성된 코드가 반복되는 횟수는 $O(n)$ 이 된다.


<br/>
<br/>

## &#128161; Check Point
- 이 문제는 탐욕법으로 풀이가 가능하다.
- 탐욕법이 가능하다라는 것은 앞 단계에서의 선택(앞 자리에 큰 수)이 이 후 단계에서의 동작에 의한 해(solution) 의 최적성(optimality) 에 영향을 주지 않기에 탐욕법이 가능하다고 말하는 것이다.
- 따라서, 어떤 문제가 주어졌을 때 가능한 모든 조합을 조사하지 말고 한 방향으로 조사하면서 지금 가장 최적의 해를 만들 수 있으리라고 여기는 동작을 채택하면서 진짜 최적의 해를 찾아나갈 수 있다면 탐욕법이 적용 가능한 문제인 것이다!!