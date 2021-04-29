---
title: "[Programmers Dev] 좌표계 변환 (Change of Basis) "
excerpt: "인공지능 수학"
toc: true
toc_sticky: true
categories:
 - DL
tags:
 - 프로그래머스
 - 인공지능
 - 선형대수
use_math: true
---

## &#128161; 좌표계 변환 (Change of Basis)

- 좌표계 :: 좌표값 = 행렬 :: 벡터 의 개념과 같다.

좀 더 이해하기 쉽게 예를 들자면 다음과 같다.

<br/>

$A\mathbf{x} = b$ 일 때, 

<br/>

- $A$는 <code>좌표계</code>를 의미한다.
- $\mathbf{x}$ 는 <code>좌표계에서 좌표값</code>의 의미를 가진다.
- $b$ 도 <code>좌표값</code>을 의미한다.
- $b$ 의 좌표계는 $I$ <code>(항등행렬)</code> 이다.

<br/>

#### 벡터의 수학적 표현

- 좌표계를 도입한 후, 벡터의 시작점을 원점에 맞추고 끝점의 위치를 벡터 $v$ 의 수학적 표현으로 정의한다.
- $v$ 의 크기: 화살표의 길이를 계산
- $v$ 의 방향: 화살표의 방향을 벡터로 표현

<br/>

### &#128204; 좌표계 변환 (Change of Basis) 

- (우항): 표준좌표계 (standard coordinate system) 에서 어떤 벡터의 좌표값은 $b$ 이다.
- (좌항): $A$ 의 열벡터들을 기저 (basis) 로 가지는 좌표계에서는 동일 벡터의 좌표값은 $\mathbf{x}$ 이다.

<br/>

역행렬을 이용해 선형시스템의 해를 구하는 문제 역시 좌표계 변환으로 바라볼 수 있다.

<br/>

$A\mathbf{x} = b$ : 기준이 $b$ 이다.

- (좌항): 표준좌표계 에서 어떤 벡터의 좌표값은 $\mathbf{x}$ 이다.

$A^{-1}b = \mathbf{x}$ : 기준이 $\mathbf{x}$ 이다.

- (좌항): $A^{-1}$ 의 열벡터들을 기저 (basis) 로 가지는 좌표계에서는 동일 벡터의 좌표값은 $b$ 이다.

<br/>

따라서,

<br/>

$A\mathbf{x} = b$ 

<br/>

- (우항): 표준좌표계에서 어떤 벡터의 좌표값은 $b$ 이다.
- (좌항): $A$ 의 열벡터들을 기저(basis) 로 가지는 좌표계에서는 동일 벡터의 좌표값은 $\mathbf{x}$ 이다.

<br/>

예제) 좌표계 변환(Change of Basis)

$2$- 벡터 $v$ 가 표준좌표계에서 $(2,3)$ 으로 표현된다고 하자.

벡터 $(3,1)$ 과 $(1, -2)$ 를 기저벡터로 가지는 새로운 좌표계를 도입했을 때, 해당 벡터 $v$ 는 어떤 좌표값을 가지는가?

<br/>
$$
\left[
\begin{matrix}
    3 & 1 \\
    1 & -2
\end{matrix}
\right]\left[
\begin{matrix}
    v_1 \\
    v_2
\end{matrix}
\right]
$$
<br/>
$$
v_1\left[
\begin{matrix}
    3 \\
    1
\end{matrix}
\right] + v_2\left[
\begin{matrix}
    1 \\
    -2
\end{matrix}
\right] = 2\left[
\begin{matrix}
    1 \\
    0
\end{matrix}
\right] +3\left[
\begin{matrix}
    0 \\
    1
\end{matrix}
\right]
$$
<br/>
$$
v = \left[
\begin{matrix}
    1 \\
    -1
\end{matrix}
\right]
$$
<br/>

> &#128173; 위와 같은 방식으로 벡터 $v$ 의 좌표값을 구할 수 있다.

<br/>

<br/>

## &#128161; Check Point

- 행렬은 <code>좌표계</code>이고, 벡터는 <code>좌표값</code>이다.
- 임의의 $v$ 는 다양한 좌표계에서 표현될 수 있다.

<br/>
$$
(I) V = A V_A
$$
<br/>

> &#128173; (표준좌표계에서 표현된 v )= (좌표계 $A$) (좌표계 $A$ 에서 표현된 $v$)

<br/>
$$
(I)V = BV_B
$$
 <br/>

> &#128173; (표준좌표계에서 표현된 v) = (좌표계 $B$)(좌표계 $B$ 에서 표현된 $v$)