---
title: "[Programmers Dev] 행렬 표기법과 관련 용어 "
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

## &#128161; 행렬 표기법과 관련 용어

### &#128204; 행렬 (matrix)

- 직사각형 구조에 숫자들을 담아 놓은 구조이다.

- 각 숫자들은 행렬의 요소 (entry) 라 부른다.

<br/>

다음은 3개의 행 (row) 과 2 개의 열 (column) 으로 이루어진 $3 \times 2$ 행렬이다.

<br/>
$$
\left[
\begin{matrix}
    3 & 1 \\
    1 & -2 \\
    2 & -4
\end{matrix}
\right]
$$
<br/>

다음과 같이 하나의 행 혹은 하나의 열을 가지는 특별한 행렬을 생각할 수 있다.

> &#128173; 각각 행벡터 (row vector), 열벡터 (column vector) 라 한다.

<br/>
$$
\left[
\begin{matrix}
    2 & 1 & 0 & -3 
\end{matrix}
\right]
\quad \quad \quad\left[
\begin{matrix}
    1  \\
    3  \\
    2 
\end{matrix}
\right]
$$
<br/>

극단적으로 $1 \times 1$ 행렬을 생각할 수 있는데, 이는 스칼라 (scalr) 와 같다.

<br/>
$$
[4]
$$
<br/>

$m \times n$ 행렬은 다음과 같이 $(m \times n)$ 개의 숫자가 직사각형 구조에 채워진 행태로 표기할 수 있다.

<br/>
$$
A = \left[
\begin{matrix}
    a_{11} & a_{12} & a_{13} & ...& a_{1n} \\
    a_{21} & a_{22} & a_{23} & ... &a_{2n} \\
      &&...  \\
      a_{m1} & a_{m2} & a_{m3} & ...& a_{mn}
\end{matrix}
\right]
$$
<br/>

**주요 표기법**

- 행렬 A 의 각 $(i,j)$- 요소는 $a_{ij}$ 로 나타낸다.
- 행렬 A 를 간략히 표기할 때는 $A = [a_{ij}]$ 로 나타낸다.
- 행렬 A 의 크기가 중요할 경우는 $A = [a_{ij}]_{m\times n}$ 로 나타낸다.

<br/>

### &#128204; Transpose Matrix (전치행렬)

- $m \times n$ 행렬 A 에 대한 transpose matrix  $A^T$ 는 $A$ 의 행을 열로, $A$ 의 열을 행으로 가지는 

  $n \times m$ 행렬이다.

- $A^T_{ij} = A_{ij}$ 를 만족한다.

예)

<br/>
$$
A = \left[
\begin{matrix}
    1 & 2 \\
    3 & 4 \\
    5 & 6
\end{matrix}
\right] \quad \quad \quad A^T = \left[
\begin{matrix}
    1 & 3  & 5\\
    2 & 4 & 6 \\   
\end{matrix}
\right]
$$
<br/>

### &#128204; 벡터 표기법

- 벡터는 아래의 $\mathbf{x}$ 와 같이 볼드체 소문자로 표기한다.

<br/>
$$
\mathbf{x} = \left[
\begin{matrix}
    \mathbf{x_1}  \\
    \mathbf{x_2}  \\
    ..\\
    \mathbf{x_n}   
\end{matrix}
\right]
$$
<br/>

**주요 표기법**

- 벡터라고 하면 일반적으로 열벡터 (column vector) 를 말한다.
- $n$- 벡터는 $n$ 개의 스칼라 (scalar) 로 구성된 벡터를 말한다.

<br/>

### &#128204; Zero Matrices (영행렬)

- 행렬의 모든 요소가 0 이면, 해당 행렬을 영행렬 (zero matrix) 라 하고 $O$ 으로 표기한다.

<br/>
$$
A + O = O + A = A
$$
<br/>

> &#128173; 영행렬은 숫자의 0 과 같은 존재로 행렬합에 대한 항등원 역할을 한다.

<br/>

**행렬의 합**

- 두 행렬 A 와 B 는 행과 열의 개수가 모두 같을 때 성립하며, 각 $(i,j)$- 요소의 합으로 정의된다.

<br/>

### &#128204; $n \times n$ 행렬: Square Matrix (정방행렬)

- 행과 열의 개수가 모두 $n$ 인 정사각형 모양의 행렬을 $n$ 차 square matrix 라 한다.

<br/>
$$
A = \left[
\begin{matrix}
    a_{11} & a_{12} & a_{13} & ...& a_{1n} \\
    a_{21} & a_{22} & a_{23} & ...& a_{2n} \\
      &&...  \\
      a_{n1} & a_{n2} & a_{n3} & ... &a_{nn}
\end{matrix}
\right]
$$
<br/>

> &#128173; 특히, $a_{ii} (i = 1, 2,..n)$ 를 행렬 $A_n$ 의 main diagonal (주대각선) 이라 한다.

<br/>

### &#128204; Identity Matrices (항등행렬)

- 주대각선이 1 이고 나머지 요소는 모두 0 인 $n$ 차 정방행렬을 identity matrix 라 한다.

<br/>
$$
A = \left[
\begin{matrix}
    1 & 0 & 0 & ...& 0 \\
    0 & 1 & 0 & ... &0 \\
      &&...  \\
      0 & 0 & 0 & ...& 1
\end{matrix}
\right]
$$
<br/>

> &#128173; 항등행렬은 숫자의 1 과 같은 존재로 행렬곱에 대한 항등원 역할을 한다.

<br/>

### &#128204; 행렬의 곱

- $m \times r $ 행렬 $A = [a_{ij}]$  와 $r \times n $ 행렬 $B = [b_{ij}] $ 가 있을 때, 두 행렬의 곱 $AB $ 는

  아래와 같은 $ m \times n $ 행렬 $C = [c_{ij}] $ 를 정의한다.

<br/>
$$
\left[
\begin{matrix}
    * & * &.. &* \\
   .. & ..& &..\\
    a_{i1} & a_{i2} &..& a_{ir}\\
   .. & ..&&..\\
    * & * & ..&* \\
\end{matrix}
\right]_{m \times r}   \left[
\begin{matrix}
    * & .. &b_{1j}&..& * \\
    * & .. &b_{2j}&..& *\\
    .. &  &..&&.. \\
    * &.. &b_{rj}&..& *
\end{matrix}
\right]_{r \times n}  = \left[
\begin{matrix}
    *&.. & * &..& * \\
    .. &  & c_{ij} &..\\
    * & .. & *& ..
\end{matrix}
\right]_{m \times n}
$$
<br/>
$$
AB = C
$$


<br/>

- 곱의 왼쪽에서는 행단위, 오른쪽에서는 열 단위로 뽑아온다.
- 곱의 왼쪽에서의 열의 개수와, 오른쪽에서의 행의 개수가 같아야 연산이 가능하다.
- $c_{ij}$ 는 각 요소의 내적과 같다.

<br/>

**행렬의 곱에서 반드시 숙지해야할 사항**

행렬의 곱은 곱의 왼쪽 행렬 $A$ 의 $i$ 번째 행벡터와 곱의 오른쪽 행렬 $B$ 의 $j$ 번째 열벡터의 내적이다.

- 따라서, 두 행렬의 곱 $AB$ 에 대해 $A$ 의 열 개수와 $B$ 의 행 개수는 일치해야 한다.
- 일반적으로 $ AB\neq BA$ 이다.

> &#128173; 행과 열을 뽑아오는 방법이 다르기 때문!

행렬의 곱은 병렬처리 (parallel processing) 로 가속할 수 있다.

> &#128173; 이러한 구현에 따라 인공지능 프로그램을 학습의 가속이나 테스트의 가속 등 좀 더 빠른 프로그램으로 구상할 수 있다.

<br/>

#### 스칼라 $ \rightarrow $ 벡터 $\rightarrow$ 행렬

- 스칼라는 숫자 하나로 구성되어 있다.

<br/>

$7$

<br/>

- 이 스칼라를 벡터로 표현하면 1개의 구성요소로 이루어진 $1$- 벡터가 된다.

<br/>

$[7]$

<br/>

- 이 스칼라를 행렬로 표현하면 1개의 구성요소로 이루어진 $1 \times 1 $ 행렬이 된다.

<br/>

$[7]_{1 \times 1}$

<br/>

#### 벡터 $ \rightarrow $ 행렬

- 벡터는 여러 숫자가 일열로 늘어선 구조이다.

<br/>
$$
\left[
\begin{matrix}
    1  \\
    2  \\
    3\\
    4 
\end{matrix}
\right]
$$
<br/>

- 이 벡터를 행렬로 표현하면 다음과 같이 여러 모양의 행렬로 표현할 수 있다.

<br/>
$$
\left[
\begin{matrix}
    1  \\
    2  \\
    3\\
    4 
\end{matrix}
\right]_{4 \times 1}\quad \quad \left[
\begin{matrix}
    1 & 2  \\
    3 & 4  \\ 
\end{matrix}
\right]_{2 \times 2} \quad \quad \left[
\begin{matrix}
    1 & 3  \\
    2 & 4 \\
\end{matrix}
\right]_{2 \times 2} \quad \quad \left[
\begin{matrix}
    1 &2&3&4
\end{matrix}
\right]_{1 \times 4}
$$
<br/>

> &#128173; 표현하고자 하는 행렬의 모양은 응용문제에 따라 결정하게 된다.

<br/>

#### 행렬 $\rightarrow$ 벡터

- 행렬은 사각형 구조에 여러 숫자가 행과 열로 늘어선 구조이다.

<br/>
$$
\left[
\begin{matrix}
    1 & 2 &3 \\
    4 & 5& 6
\end{matrix}
\right]_{2 \times 3}
$$
<br/>

- 이 행렬은 다음과 같이 $6$- 벡터로 표현할 수 있다.

<br/>
$$
\left[
\begin{matrix}
    1 \\ 2 \\3\\4\\5\\6
\end{matrix}
\right]_{6 \times 1} \quad \quad\left[
\begin{matrix}
    1 \\ 4 \\2\\5\\3\\6
\end{matrix}
\right]_{6 \times 1}
$$
<br/>

> &#128173; 행렬을 벡터로 변환할 때, 행부터 혹은 열부터 읽을 것인지는 응용문제에 따라 결정한다.

<br/>

#### 텐서

- 텐서 (tensor) 는 스칼라, 벡터, 행렬을 아우르는 개념이다. 
- 숫자가 늘어설 수 있는 방향이 $k$ 개면 $k$- 텐서로 부른다.
  - $0$- 텐서: 스칼라
  - $1$- 텐서: 벡터
  - $2$- 텐서: 행렬

만일 아래의 $T$ 의 각 요소 $P_{(i,j)}$ 가 벡터라면, $T$ 는 $3$- 텐서로 볼 수 있다.

<br/>
$$
T = \left[
\begin{matrix}
    P_{(1,1)} & P_{(1,2)} & P_{(1,3)} & \cdots& P_{(1,j)} \\
    P_{(2,1)} & P_{(2,2)} & P_{(2,3)} & \cdots& P_{(2,j)} \\
      &&\ddots  \\
      P_{(i,1)} & P_{(i,2)} & P_{(i,3)} & \cdots &P_{(i,j)}
\end{matrix}
\right]
$$
<br/>

>  &#128173; $3$- 텐서의 대표적인 예는 컬러영상이다. $P_{(i,j)}$ 가 $3$- 벡터이면 RGB 영상을, $4$- 벡터이면 RGBA 영상을 나타낸다고 볼 수 있다.

<br/>

### &#128204; 분할행렬 (Partitioned Matrix)

- 추상적인 구조로 행렬 / 행렬연산을 파악할 때 굉장히 유용한 구조이다.

> &#128173; **행렬을 조각(partition) 단위**로 분할하여 생각해도 무방하다. 이런 관점에서 본다면, 행렬은 **부분행렬(submaxtrix)**로 이루어진 직사각형 구조로 확장해서 생각할 수 있다. 이렇게 행렬을 구조적으로 보는 방법을 <code>분할행렬(partitioned matrix)</code>code>또는 <code>블록행렬(block matrix)</code>라 한다.

<br/>
$$
A = \left[
\begin{array}{cc|c}
    a_{11} & a_{12} & a_{13} \\
   a_{21} & a_{22} & a_{23}\\   
   \hline
   a_{31} & a_{32} & a_{33}  \\
\end{array}
\right] =  \left[
\begin{array}{}
    A_{11} & A_{12} \\
   A_{21} & A_{22}\\   
\end{array}
\right]
$$
<br/>
$$
= \left[
\begin{array}{}
    a_{11} & a_{12} & a_{13} \\
    \hline
   a_{21} & a_{22} & a_{23}\\  
   \hline
   a_{31} & a_{32} & a_{33}  \\
\end{array}
\right] =\left[
\begin{matrix}
    r_1 \\ r_2 \\r_3
\end{matrix}
\right]
$$
<br/>

>  &#128173; 행벡터의 모음으로 보는 경우: 열벡터로 표현

<br/>
$$
= \left[
\begin{array}{c|c}
    a_{11} & a_{12} & a_{13} \\
   a_{21} & a_{22} & a_{23}\\  
   a_{31} & a_{32} & a_{33}  \\
\end{array}
\right] =\left[
\begin{matrix}
    c_1 & c_2 &c_3
\end{matrix}
\right]
$$

> &#128173; 열벡터의 모음으로 보는 경우: 행벡터

&#128073; 열벡터를 기준으로 보는 관점, 3 번째 관점이 제일 많이 쓰이는 관점이다.

<br/>

#### 분할행렬로 행렬의 곱 이해하기

- 두 행렬의 곱 $AB=C$ 를 아래와 같이 두 가지 관점으로 볼 수 있다.

1) column vector - matrix product

<br/>
$$
AB = A[b_1b_2  \cdots b_n] = [Ab_1 Ab_2\cdots Ab_n] = C
$$
<br/>

> &#128173; 결과행렬의 첫 번째 열은 $A \times b_1$ 의 내적, 두 번째 열은 $A \times b_2$ 의 내적의 결과이다.

<br/>

2) row vector - matrix product

<br/>
$$
AB = \left[
\begin{matrix}
    a_1 \\ a_2 \\\vdots\\a_m
\end{matrix}
\right]B = \left[
\begin{matrix}
    a_1B \\ a_2B \\\vdots\\a_mB
\end{matrix}
\right] = C
$$
<br/>

> &#128173; 결과행렬의 첫 번째 행은 $a_1 \times B$ 의 내적, 두 번째 열은 $a_2 \times B$ 의 내적의 결과이다.

<br/>

<br/>

### &#128204; 선형조합 (Linear Combination):

- $A \mathbf{x}$ 는 $A$ 의 열벡터에 대한 선형조합이다.

> &#128173; '행렬은 vector 들의 모임이다' 라는 관점에서 보게되면 $A$ 를 구성하는 열벡터들의 중심으로 볼 수 있다. 그럴경우 $A$ 의 열벡터들의 가중치를 $\mathbf{x}$ 와의 관계라고 볼 수 있다.

행렬을 구조적으로 바라보는 가장 효과적인 방법은 다음과 같다.

<br/>

행렬은 열벡터의 리스트이다.

<br/>
$$
A = \left[
\begin{matrix}
    a_{11} & a_{12} & a_{13} & \cdots & a_{1n} \\
    a_{21} & a_{22} & a_{23} & \cdots& a_{2n} \\
      && \ddots  \\
      a_{m1} & a_{m2} & a_{m3} & \cdots &a_{mn}
\end{matrix}
\right] = [a_1 a_2\cdots a_n ]
$$
<br/>

> &#128173; 여기서 $a_i$ 는 행렬 $A$ 의 $i$- 번째 열벡터이다. 특히 각 열벡터는 $m$- 벡터이기 때문에,
>
> <span style="background-color:#fffacd">**$m \times n $ 행렬은 $m$- 벡터가 $n$ 개 있다**</span> 고 해석하면 된다.

<br/>

#### 행렬 @ 벡터 연산을 구조적으로 보기

- $A \mathbf{x}$ 는 행렬 $A$ 가 가지고 있는 열벡터의 선형조합이다.

<br/>
$$
A = \left[
\begin{matrix}
    a_{11} & a_{12}  & \cdots & a_{1n} \\
    a_{21} & a_{22} & \cdots& a_{2n} \\
      && \ddots  \\
      a_{m1} & a_{m2}  & \cdots &a_{mn}
\end{matrix}
\right]\left[
\begin{matrix}
    \mathbf{x}_1 \\ \mathbf{x}_2 \\\vdots\\\mathbf{x}_n
\end{matrix}
\right] = [a_1 a_2\cdots a_n ]\left[
\begin{matrix}
    \mathbf{x}_1 \\ \mathbf{x}_2 \\\vdots\\\mathbf{x}_n
\end{matrix}
\right] = \mathbf{x}_1a_1 +\mathbf{x}_2a_2 + \cdots \mathbf{x}_na_n
$$
<br/>

> &#128173; 선형대수에서는 이처럼 벡터들에 대한 가중치 합을 특히 <span style="background-color:#fffacd">**선형조합 (linear combination)**</span> 이라 부른다.

&#128073; $A \mathbf{x}$ 의 결과는 행렬 $A$ 가 가지고 있는 열벡터의 선형조합에서만 나올 수 있다. 

<br/>

#### 선형시스템 $A \mathbf{x} = b$ 를 선형조합 관점에서 바라보기

- 행렬 $A$ 의 열벡터를 가중치합으로 선형조합할 때, 벡터 $b$ 를 만들 수 있는 가중치 조합이 존재한다면, 선형시스템 $A \mathbf{x} = b$ 의 해는 존재한다. 그 해는 가중치 $\mathbf{x}_i$ 들로 구성된 $\mathbf{x} $ 이다.

> &#128173; 가중치 조합이 존재하지 않는다면 선형시스템 문제의 해는 존재하지 않는 것이다.

<br/>

**Column Space (열공간)**

- 행렬 $A$ 의 열벡터들에 대한 가능한 모든 선형조합의 결과를 모아 집합으로 구성할 수 있다.
- 이 지합을 column space 이라 하고 다음과 같이 표현한다.

<br/>
$$
col(A)
$$
<br/>

**Consistent Linear System**

- 선형시스템 $A\mathbf{x} = b$ 가 해를 가지면 (consistent), 다음을 만족한다.

<br/>
$$
b \in col(A)
$$
<br/>

**Inconsistent Linear System**

- 선형시스템 $A \mathbf{x} =b$ 가 해가 없으면 (inconsistent), 다음을 만족한다.

<br/>
$$
b \notin col(A)
$$
<br/>

예제) Column Space (열공간)

- 아래 행렬 $A$ 의 $col(A)$ 은 $3$- 차원 공간이다.

<br/>
$$
A = \left[
\begin{matrix}
    -1 & 3 & 2 \\
    1 & 2 & -3 \\
    2 & 1 & -2
\end{matrix}
\right]
$$
<br/>

> &#128173; 따라서 어떤 $3$- 벡터 $b$ 를 이용해 선형시스템 $A \mathbf{x} = b$ 를 구성한다고 하더라도, 해당 선형시스템의 해는 존재한다.

<br/>

- 아래 행렬 $A$ 의 $col(A)$ 는 $xy$- 평면이다.

<br/>
$$
A = \left[
\begin{matrix}
    -1 & 3 & 2 \\
    1 & 2 & -3 \\
    0 &  0& 0
\end{matrix}
\right]
$$
<br/>

> &#128173; 따라서 $xy$- 평면 상의 $3$- 벡터 $b$ 를 이용해 선형시스템 $A \mathbf{x} =b $ 를 구성하면, 해당 선형시스템의 해는 존재한다.
>
> 그러나 $xy$- 평면을 벗어난 $3$- 벡터 $b$ 를 이용해 선형시스템 $A\mathbf{x} = b$ 를 구성하면, 해당 선형시스템의 해는 존재하지 않는다.

<br/>

<br/>

## &#128161; Check Point

- 행렬에 대한 기본 구조와 여러 종류를 정확히 파악해두기!
- 특히, 행렬의 곱은 **병렬처리**로 가속할 수 있다는 점을 항상 숙지해서 이후에 활용해보기!
- 분할행렬의 개념으로 선형조합의 개념을 이해하고 해당 관점에서 선형시스템을 바라볼 것!