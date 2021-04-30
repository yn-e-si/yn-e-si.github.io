---
title: "[Programmers Dev] 벡터공간과 최소제곱법 "
excerpt: "인공지능 수학"
toc: true
toc_sticky: true
categories:
 - DL
tags:
 - 프로그래머스
 - 인공지능 수학
 - 선형대수
use_math: true
---

## &#128161; 벡터공간과 최소제곱법

벡터공간을 정의하기 전에 몇 가지 용어에 대해 먼저 정의해보자.

<br/>

**집합 (set)**

집합 (set) 은 임의의 원소 (element) 를 수집하여 만든 모듬이다.

<br/>

**연산에 닫혀 있는 집합**

어떤 연산을 생각한 다음, 집합에서 임의의 원소를 뽑아 연산을 수행한 결과가 여전히 집합의 원소로 있다면, 해당 집합은 연산에 닫혀 있다고 한다.

<br/>

$\{x\mid x \in \mathbb{R} \}$

<br/>

- 위의 집합은 덧셈 연산과 곱셈 연산에 닫혀 있다.

<br/>

$\{-1,0,1\}$

<br/>

- 위의 집합은 연산에는 닫혀 있지 않지만, 곱셈 연산에는 닫혀있다.

<br/>

**공간 (space)**

공간은 다음의 두 연산에 닫혀 있는 집합이다.

- 덧셈연산에 닫혀 있다

> &#128173; 집합에서 임의의 두 원소 $x,y$ 를 뽑아 더해도 그 결과 $x+y$ 는 집합의 원소이다.

- 스칼라 곱 연산에 닫혀 있다

> &#128173; 집합에서 임의의 한 원소 $x$ 를 뽑아 임의의 스칼라 $s$ 배 한 결과 $sx$ 는 집합의 원소이다.

<br/>

다음과 같이 $n$- 벡터의 집합은 모두 공간이다.

<br/>
$$
\mathbb{R}^n = \{x \mid x = (x_1,x_2, ...,x_n), (단, x_i \in \mathbb{R})\}
$$
<br/>

&#128073; **<span style="background-color:#fffacd">모든 $n$- 벡터 집합 $\mathbb{R}^n$ 은 $n$ 차원 벡터 공간 (vector space)</span>**라 부를 수 있다.

<br/>

**열공간 (Column Space)**

행렬 $A$ 의 열벡터들에 대한 가능한 모든 선형조합의 결과를 모아 집합으로 구성할 수 있는데,

이 집합을 column space 라 하고 다음과 같이 표기한다.

<br/>

$col(A)$

<br/>

**Consistent Linear System**

선형시스템 $A \mathbf{x} = b$ 가 해를 가지면, 다음을 만족한다.

<br/>

$b \in col(A)$

<br/>

**Inconsistent Linear System**

선형시스템 $ A \mathbf{x} = b$ 가 해가 없으면, 다음을 만족한다.

<br/>

$b \notin col(A)$

<br/>

<br/>

### &#128204; 최소제곱법 (least squares method)

> &#128173; 최소제곱법을 바로 정의하기전에 최소제곱법의 아이디어에 대해 논하고자 한다.
>
> <br/>
>
> 앞서 배웠던 선형시스템 $A \mathbf{x} = b$ 에서 해가 없을 경우에 대해서 구할 수 없다라는 결론을 내고 지나왔다. 하지만 **해가 없음에도 불구하고 우리가 할 수 있는 최선이 무엇인가**를 생각해보자.
>
> <br/>
>
> 행렬 $A$ 가 정의하는 열공간에서 우리의 목표 $b$ 와 가장 가까운 지점은 $b$ 를 열공간에 투영 (projection) 한 저점일 것이다. 즉, **달성가능한 최선의 목표 $proj_wb$** 를 생각할 수 있다.
>
> <br/>
>
> &#128073;  $b$ 를 직접적으로 구하는 것이 아닌 **<span style="background-color:#fffacd">구할 수 있는 공간 (column space) 에 projection 한 값</span>**을 구한다는 것이다!

<br/>

최소젭곱법은 선형시스템 $A \mathbf{x} = b$ 에 대한 해 $\mathbf{x}$ 가 없음에도 불구하고, 할 수 있는 최선의 대안

$\bar{\mathbf{x}}$ 을 내놓는 기법이다. 최소제곱법은 원래의 선행시스템 $ A \mathbf{x} = b$ 가 아닌 다음의 선형시스템을 해결한다.

<br/>
$$
A\bar{\mathbf{x}} = \bar{\mathbf{b}} (단, \bar{\mathbf{b}} = proj_w\mathbf{b})
$$
<br/>

이 방법은 목표 $b$ 와 달성가능한 목표 $\bar b$ 의 차이를 나타내는 벡터 $ (b- \bar b)$ 의 제곱길이를 최소하시키는 의미를 가지기 때문에 최소제곱법 (least squares method) 이라 불리운다.

<br/>

주어진 선형시스템의 양변에 전치행렬 $A^T$ 를 곱하면 최소제곱법의 해를 구할 수 있다.

<br/>
$$
A\mathbf{x} = b
$$
<br/>
$$
\Rightarrow A^TA\bar{\mathbf{x}} = A^Tb
$$
<br/>
$$
\Rightarrow \bar{{\mathbf {x}}} = {(A^TA)^{-1}}A^Tb
$$
<br/>

&#128073; 양변에 전치행렬을 곱하면 문제가 $\mathbf{x}$ 를 구하는 것에서 $\bar{ \mathbf{x}}$  를 구하는 것으로 바뀐다.

<br/>

다만 여기서 꼭 기억해야할 것이 있다. 최소제곱법으로 구한 해 $\bar { \mathbf{x}}$ 는 원래의 선형시스템을 만족하는 해는 아니다. 우리가 구할 수 있는 것은 <code>column space</code> 에 있는 것들만 구할 수 있기 때문이다.

<br/>

$A \bar {\mathbf{x}} \neq b$

<br/>

최소제곱법으로 구한 해 $ \bar{ \mathbf {x}}$ 는 다음을 만족하는 <code>근사해 (approximate solution)</code> 이다.

<br/>

$A \bar { \mathbf{x}} = proj_Wb$

<br/>

#### 최소제곱법의 응용: 선형회귀 (Linear Regression)

2 차원 공간에 4 개의 정점 $(-3,-1),(-1,-1),(1,3),(3,3) $ 이 있을 때, 이를 잘 설명할 수 있는 직선 $y = mx +b$ 를 구하는 문제를 선형회귀 문제라 한다.

&#128073; 모든 정점을 지나는 직선은 존재하지 않으나 모든 정점을 고려했을 때 가장 잘 설명할 수 있는 가상의 직선을 찾는 것이다.

<br/>

이를 풀기위해서 다음의 과정을 거친다.

<br/>

- 선형시스템 구성: 직선이 각 정점을 모두 지나간다고 가정하고 선형시스템 $ A\mathbf{x} = b$  구성한다.

> &#128173; 단, 주어진 모든 정점을 지나가는 직선은 존재하지 않으므로 선형시스템의 해는 존재하지 않는다.

<br/>
$$
y = mx +b
$$
<br/>
$$
\left[
\begin{matrix}
    -3 & 1  \\
    -1 & 1 \\
     1 & 1 \\
     3&1  
\end{matrix} \right] \left[
\begin{matrix}
    m  \\
    b \\ 
\end{matrix} \right] =\left[
\begin{matrix}
    -1   \\
    -1  \\
     3 \\
     3  
\end{matrix} \right] 
$$
<br/>

- 최소제곱법 적용: $A^TA \bar{ \mathbf{x}} = A^Tb$ 를 생각하고, $\bar {\mathbf{x}} = \left[ \begin{matrix}    \bar{m}   \\    \bar{b}  \\       \end{matrix} \right] $ 를 구한다.

> &#128173; 원래는 $(4\times2)(2 \times1) = (4\times1)$ 문제였지만 $(2 \times4)(4\times2)(2 \times1) = (2 \times4)(4 \times1)$ 로 바뀜에 따라 $(2 \times1)$ 을 구하는 문제로 바뀌게 되었다.



<br/>

<br/>

## &#128161; Check Point

- 벡터공간은 선형시스템의 해가 존재할 수 있는 범위와도 같다.
- 최소제곱법은 선형시스템의 해가 존재하지 않을 때, 현재 주어진 선형시스템에서의 가장 근접한 해를 도출해내기 위한 방법이다.