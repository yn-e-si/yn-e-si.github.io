---
title: "[Programmers Dev] 통계학, 기본개념 "
excerpt: "인공지능 수학"
toc: true
toc_sticky: true
categories:
 - DL
tags:
 - 프로그래머스
 - 인공지능 수학
 - 통계학
use_math: true
---

## &#128161; 통계학, 기본개념

### &#128204; 개념 정의

**통계학**

- 데이터의 수집 (collection), 구성 (organization), 분선 (analysis), 해석 (interpretation), 표현 (presentation) 에 관한 학문이다.
- 통계학은 크게 두 부류로 나뉜다.
  - 기술통계학 (descriptive statistics)
  - 추측통계학 (inferential statistics)

&#128073; 다시 말해, 통계학은 데이터를 수집해서 잘 표현한 다음 분석을 해서 미래를 예측하려는 학문이라 할 수 있다.



<br/>

**모집단 (population)**

- 어떤 질문이나 실험을 위해 관심의 대상이 되는 개체나 사건의 집합이다.
- ex) 전교 남학생의 키

**모수 (parameter)**

- 모집단의 수치적인 특성을 말한다.
- ex) 키의 평균

**표본 (sample)**

- 모집단에서 선택된 개체나 사건의 집합

&#128073; 보통 알고 싶어하는 것은 모수이지만 모집단 전체의 정보를 알 수 있는 경우가 거의 없기에 표본을 통해서 모수를 추정하게 된다.

> &#128173; 모집단 전체를 조사하기엔 시간, 비용이 많이 들기 때문이다.

<br/>

**도수 (Frequency)**

- 정의
  - 어떤 사건이 실험이나 관찰로부터 발생한 횟수를 의미한다.
- 표현 방법
  - 도수분포표 (Frequency Distribution Table)
  - 막대그래프 (Bar graph)
    - 질적 자료 (각각의 값들이 범주로 되어있는 자료)
  - 히스토그램 (Histogram)
    - 양적 자료 (모집단의 값들이 숫자들인 자료)

<br/>

**상대도수**

- 도수를 전체 원소의 수로 나눈 것이다.
- 상대도수의 합은 항상 1이 된다.

<br/>



**줄기 잎 그림 (Stem and Leaf Diagram)**

- 양적 자료를 줄기와 잎으로 구분해서 시각적으로 표현한 그림이다.

<br/>

**평균 (Mean)**

- 모평균 m
    - 모집단 전체 자료일 경우
- 표본 평균 $\bar{x}$
    - 모집단에서 추출한 표본일 경우

<br/>

**python code**

```python
import statistics
a = [79, 54, 74, 62, 85, 55, 88, 85, 51, 85, 54, 84, 78, 47]
statistics.mean(a)
```

<br/>



**중앙값 (Median)**  

- 평균의 경우 극단 값의 영향을 많이 받는 단점이 있는데, 이를 보완한 수치이다.
- 주어진 자료를 높은 쪽 절반과 낮은 쪽 절반으로 나누는 값을 의미한다.
- 자료를 순서대로 나열했을 때 가운데 있는 값이다.
- 자료의 수: $n$
    - $n$ 이 홀수: $\frac{(n+1)}{2}$ 번째 자료값
    - $n$ 이 짝수: $\frac{n}{2}$ 번째와 $\frac{n}{2}+1$ 번째 자료값의 평균

<br/>

**python code**

```python
a = sorted(a)
statistics.median(a)
```

<br/>

**분산 (Variance)**

- 산포의 정도를 정량화 시킨 것을 의미한다.
- 편차의 제곱의 합을 자료의 수로 나눈 값이다.
    - 편차: 값과 평균의 차이
- 자료가 모집단일 경우: 모분산
$$\sigma^2 = \frac{1}{N} \sum^N_{i=1} (x_i - m)^2$$
- 자료가 표본일 경우: 표본분산
$$s^2 = \frac{1}{n-1} \sum^N_{i=1} (x_i - \bar{x})^2$$

&#128073; 분산의 값을 보면 자료들이 평균에 비해 얼마나 퍼져 있는지 알 수 있다.

<br/>

**python code**

```python
# 모분산을 구해준다.

방법 1.
statistics.pvariance(a)

방법 2.
numpy.var(a)


# default 로 표본분산을 구해준다.
방법 1.
statistics.variance(a)

방법 2.
import scipy
import scipy.stats
scipy.stats.tvar(a)

방법 3.
# ddof: Delta Degrees of Freedom
numpy.var(a, ddof=1)

```

<br/>

**표준편차 (Standard Deviation)**

- 분산의 양의 제곱근
- 모표준편차 (population standard deviation)
$$\sigma = \sqrt{\frac{1}{N} \sum^N_{i=1} (x_i - m)^2}$$
- 표본표준편차 (sample standard deviation)
$$s =\sqrt{ \frac{1}{n-1} \sum^N_{i=1} (x_i - \bar{x})^2}$$

<br/>

**python code**

```python
# 모표준편차

방법 1.
statistics.pstidev(a)

방법 2.
numpy.std(a)

# 표본표준편차

방법 1.
statistics.stdev(a)

방법 2.
# ddof: Delta Degrees of Freedom
numpy.std(a. ddof=1)
```

<br/>

**범위 (Range)**

- 자료를 정렬하였을 때 가장 큰 값과 가장 작은 값의 차이를 의미한다.
- 극단값이 있을 경우 범위가 굉장히 커지는 단점이 존재한다.
- 이럴 경우 사분위수를 활용해서 이러한 단점을 보완할 수 있다.



<br/>

python code

```python
max(a) - min(a)
```



<br/>

**사분위수 (Quartile)**

- 전체 자료를 정렬했을 때 $ \frac {1}{4}, \frac{1}{2}, \frac{3}{4} $ 위치에 있는 숫자를 의미한다.
  - Q1: 제 1 사분위수
  - Q3: 제 3 사분위수
- 사분위 범위 (IQR, interquartile range)
  - Q3 - Q1 을 의미한다.
  - 이상점이 존재할 때, 유용하게 사용 가능하다.



<br/>

**python code**

```pyrhon
# 제 1 사분위수
numpy.quantile(a, .25)

# 제 3 사분위수
numpy.quantile(a, .75)

# 사분위 범위
numpy.quantile(a, .75) - numpy.quantile(a, .25)
```

<br/>

**$z$- score**

- 어떤 값이 평균으로부터 몇 표준편차 떨어져 있는지를 의미하는 값을 말한다.
  - 모집단

    ​    $$z = \frac{x-\mu}{\sigma}$$

  - 표본의 경우

    ​    $$z = \frac{x-\bar{x}}{s}$$

<br/>

**python code**

```python
# 모집단
scipy.stats.zscore(a)

# 표본집단
scipy.stats.zscore(a, ddof=1)
```



<br/>

<br/>

### &#128204; 확률 (probability)

- 상대 도수에 의한 정의

  - 똑같은 실험을 무수히 많이 반복할 때, 어떤 일이 일어나는 비율을 말한다.
    - 즉, 상대도수의 극한
  - ex) 다음날 비가 올 확률?

- 고전적 정의

  - 표본 공간 (sample space)
    - 모든 가능한 실험결과들의 집합을 말한다.
    - 예) 주사위의 숫자: $\{1,2,3,4,5,6\}$

  - 사건
    - 관심있는 실험결과들의 집합을 말한다.
    - 표본 공간의 부분집합이다.
    - 예) 주사위의 숫자 중 짝수: $\{2,4,6\}$
  - 어떤 사건이 일어날 확률
    - 표본 공간의 모든 원소가 일어날 확률이 같은 경
    - $\frac {사건의 원소의 수}{표본공간의 원소의 수}$
  - 확률 1
    - 반드시 그 사건이 일어난다.
  - 확률 0
    - 그 사건이 절대로 일어나지 않는다.
  - 확률은 0 에서 1 사이의 값을 가진다.

<br/>



#### 확률의 계산

- 고전적 확률
  - 표본 공간의 원소의 수를 세야한다.
  - 사건의 원소의 수를 세야한다.
  - 따라서 경우의 수를 쉽게 셀 수 있는 방법이 필요한데, 이는 조합 (combination) 을 사용한다.

<br/>

##### 조합 (combination)

- 어떤 집합에서 순서에 상관없이 뽑은 원소의 집합을 말한다.
- 즉 $n$ 개 중 $r$ 개를 뽑는 조합의 수이다.

<br/>
$$
_{n}\mathrm{C}_{k} = {n \choose r} = \frac{n!}{r!(n-r)!}
$$
<br/>
$$
n! = n(n-1)(n-2)...2\cdot 1
$$
<br/>
$$
{5 \choose 2} = \frac{5 \times 4 \times 3 \times 2 \times1}{2 \times 1\times 3 \times 2 \times 1} = 10
$$
<br/>

##### 덧셈 법칙 (Addition Law)

- 주사위를 던지는 실험
  - 표본 공간: $S=\{1,2,3,4,5,6\}$
- 사건 $A$
  - 주사위의 숫자가 짝수인 사건
  - $P(A) = \frac{1}{2}$
- 사건 $B$
  - 주사위의 숫자가 4 이상인 사건
  - $P(B) = \frac{1}{2}$
- 사건 $A$ 나  사건 $B$ 가 일어날 확률
  - $A \cup B = \{2, 4, 5, 6\}$
  - $P(A \cup B) = \frac{ \mid A \cup B \mid }{ \mid S \mid} = \frac{4}{6} = \frac{2}{3}$
- 사건 $A$ 와 사건 $B$ 가 동시에 일어날 확률
  - $A \cap B = \{4, 6\}$
  - $P(A\cap B) = \frac {\mid A \cap B \mid } { \mid S \mid } = \frac {2}{6} = \frac{1}{3}$
- $P(A \cup B ) = P(A) + P(B) - P(A \cap B)$
  - $P(A \cup B) = \frac{1}{2} + \frac {1} {2} - \frac{1}{3} = \frac{2}{3}$

<br/>

##### 서로 배반 (Mutually Exclusive)

- 두 사건의 교집합이 공집합일 경우
  - 사건 $A$ 와 사건 $B$ 가 서로 배반
    - $P(A\cap B) = 0$
    - $P(A\cup B) = P(A) + P(B)$
- 사건 $A$ 
  - 주사위를 던져서 홀수가 나오는 사건
  - $\{1,3,5\}$
- 사건 $B$
  - 주사위를 던져서 4 의 배수가 나오는 사건
  - $\{4\}$
- $A$ 와 $B$ 는 서로 배반이다.
  - $P(A\cup B) = P(A) + P(B) = \frac{1}{2} + \frac{1}{6} = \frac{2}{3}$

<br/>

##### 조건부 확률 (conditional probability)

- 어떤 사건 $A$ 가 일어났을 때, 다른 사건 $B$ 가 일어날 확률

  $P(B|A) = \frac{P(A\cap B)}{P(A)}$

- 단, $P(A)>0$

예) 주사위를 하나 던졌는데, 4 이상의 수가 나왔다. 이때 그 수가 짝수일 확률은?

<br/>

- 사건 $A$
  - 4 이상의 수가 나오는 사건
    - $P(A) = \frac{3}{6} = \frac {1}{2}$
- 사건 $B$ 
  - 짝수가 나오는 사건
- $P(A \cap B) = \frac{2}{6} = \frac{1}{3}$
  - $P(B|A) = \frac{P(A\cap B)}{P(A)} = \frac{1/3}{1/2} = \frac{2}{3}$

<br/>

##### 곱셈법칙

<br/>
$$
P(B|A) = \frac{P(A\cap B)}{P(A)}
$$
<br/>
$$
P(A \cap B) = P(B|A)P(A)
$$
<br/>

> &#128173; 위의 식이 곱셈법칙이다. 이는 교집합의 확률을 조금 더 쉽게 구하기 위해 사용되는 법칙이다.

예)

어떤 학교에서 60% 의 학생이 남학생이다. 이 학교 남학생의 경우 80% 는 축구를 좋아한다.

P(A) = 0.6, P(B): 축구, P(B|A) = 0.8 

<br/>

이 학교에서 학생 1 명을 랜덤하게 뽑았을 때, 축구를 좋아하는 남학생일 확률은?

<br/>
$$
P(A \cap B) = P(B|A)P(A) = 0.8 \times0.6 = 0.48
$$
<br/>

##### 서로 독립

- $P(B|A) = P(B)$ 인 경우, 사건 $A$ 와 $B$ 는 서로 독립이다.
- 서로 독립일 경우, 아래와 같다.
  - $P(A \cap B) = P(B|A)P(A) = P(B)P(A) = P(A)P(B)$

- 주사위를 2 개 던지는 실험
  - 사건 $A$
    - 첫 번째 주사위의 숫자가 짝수인 사건
  - 사건 $B$ 
    - 두 번째 주사위의 숫자가 짝수인 사건
  - $P(A \cap B) = P(A)P(B) = \frac{1}{4}$

&#128073; $A$ 와 $B$ 가 서로 배반이면 서로 완전히 연관이 있는 것 (종속), 독립은 아니다.

> &#128173; 배반인 경우, 합집합의 확률을 조금 더 쉽게 구할 수 있다.

<br/>

##### 여사건

- 사건 $A$ 의 여사건
  - 사건 $A$ 가 일어나지 않을 사건
  - $A^C$ 로 표시
- 주사위 1개를 던지는 실험
  - 사건 $A$
    - 주사위으 숫자가 짝수인 사건
  - 사건 $A$ 의 여사건
    - 주사위의 숫자가 짝수가 아닐 사건
    - 즉, 주사위의 숫자가 홀수일 사건
- 어떤 사건과 그 여사건은 서로 배반이다.
  - 즉 들 중 하나는 반드시 일어난다.
  - $P(A \cup A^C) = P(A) + P(A^C) = 1$
  - $P(A) = 1 - P(A^C)$

<br/>

##### 확률의 분할 법칙

- 사건 $B$ 는 다음과 같이 나누어진다.
  - $B = (A \cap B) \cup (A^C \cap B)$
  - $(A \cap B) 와 (A^C \cap B)$ 는 서로 배반이다.

$$
P(B) = P[(A\cap B) \cup(A^C \cap B)] = P(A \cap B) + P(A^C \cap B)
$$

<br/>
$$
=P(B|A)P(A) + P(B|A^C)P(A^C)
$$
<br/>예)

- 어떤 사파리에서는 70% 가 사자이고, 나머지가 호랑이다.

- 사자는 60%가 2 살 이상이고, 호랑이는 40% 가 2 살 이상이다.

이 때, 전체 동물 중 2 살 이상인 동물의 비율은?

<br/>

- 사건 $A$: 동물이 사자인 사건
- 사건 $B$: 동물이 2 살 이상인 사건

$$
P(B) = P(B|A)P(A) + P(B|A^C)P(A^C) = 0.6 \times0.7 + 0.4 \times 0.3 = 0.54
$$

<br/>

##### 베이즈 정리

앞의 예제에서 동물 한 마리를 랜덤하게 선택했는데, 이 도물이 2 살 이상이었다. 이 때, 이 동물이 사자일 확률은?

- $P(A|B)= $ ?
- 위의 질문은 $P(A)$ 와는 다른 질문이다.

$$
P(A|B) = \frac {P(A \cap B)}{P(B)} = \frac{P(B|A)P(A)}{P(B|A)P(A) + P(B|A^C)P(A^C)} = \frac {0.6 \times 0.7 }{0.6 \times 0.7 + 0.4 \times 0.3 }=0.78
$$

<br/>

- 아무 정보가 없었을 때, 사자일 확률은 0.7 이지만 2살 이상이라는 추가 정보로 인해 그 확률이 0.78 이 된 것이다.

&#128073; 즉 $B$ 가 일어났을 때 $A$ 가 일어날 확률을 구하는 것을 베이즈 정리라 한다.

<br/>


$$
P(A|B) = \frac {P(A \cap B)}{P(B)} = \frac{P(B|A)P(A)}{P(B|A)P(A) + P(B|A^C)P(A^C)}
$$
<br/>

위의 식은 다음과 같이 다시 정의될 수 있다.

<br/>
$$
P(B_r|A) = \frac{P(B_r \cap A)}{P(A) } = \frac {P(B_r \cap A)}{\sum^k_{i=1}P(B_i \cap A)} = \frac {P(B_r)P(A|B_r)}{\sum^k_{i=1}P(B_i)P(A|B_j)}
$$
<br/>

- 사건 $B_1, B_2, \cdots, B_k$ 가 표본 공간 $S$ 의 분할과 같다.

> &#128173; 즉 사건 $B$ 들을 다 합칠 경우 $S$ 가 된다.

<br/>

또한 베이즈 정리는 추가적인 정보로 인해 확률이 바뀌는 경우에 종종 사용하게 된다.

- 처음의 확률:
  - 사전확률 (prior probability)
- 수정된 확률:
  - 사후확률 (posterior probability)

<br/>

예)

- 어떤 사람이 검은색과 흰색의 셔츠를 가지고 있는데, 매일 아침 $ \frac{3}{4}$ 정도는 검은색 셔츠를 입고, $\frac {1}{4} $ 정도는 흰색 셔츠를 입는다.
- 이 사람이 검은색 셔츠를 입었을 때는 $\frac{3}{4} $ 정도 넥타이를 매고, 흰색 셔츠를 입었을 때는 $\frac{1}{2}$ 정도 넥타이를 맨다고 하자.
- 어느 날 이 사람이 넥타이를 맸다면, 이 사람이 검은색 셔츠를 입었을 확률은 무엇인가?

<br/>

- 사건 $A$
  - 아침에 검은색 셔츠를 입는 사건 
  - $P(A) = \frac{3}{4}$
- 사건 $B$
  - 넥타이를 맨 사건
  - $P(B|A) = \frac {3}{4} , P(B|A^C) = \frac{1}{2}$
- 구하고자 하는 확률
  - $P(A|B) = \frac {(3/4) \times (3/4) }{(3/4) \times (3/4) + (1/2) \times (1/4)} = \frac {9}{11}$

<br/>

<br/>



## &#128161; Check Point

- 기본적인 확률의 개념 정의와 용어들을 다시 살펴보고 기억해 둘 것!!

