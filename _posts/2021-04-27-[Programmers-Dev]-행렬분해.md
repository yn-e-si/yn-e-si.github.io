---
title: "[Programmers Dev] 행렬분해 "
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

## &#128161; 행렬분해

### &#128204; LU decomposition (LU 분해)

- Gauss 소거법을 행렬의 형태로 표현한 것과 같다.
- L: lower triangular matrix (하삼각행렬)
- U: upper triangular matrix (상삼각행렬)

>  &#128173; LU 분해는 주어진 행렬 (A) 를 L 과 U 의 두 행렬의 곱으로 나누는 행렬분해이다.

<br/>
$$
AX = b
$$
<br/>

<br/>

LU 분해를 이용하면 위와 같았던 식이,

<br/>
$$
AX = b \rightarrow (LU)X = b \rightarrow L(UX) = b \rightarrow Ly=b,(단, UX = y)
$$
<br/>

<br/>

와 같은 식으로 바뀌게 된다.

&#128073; 즉, 문제 자체가 $y$ 를 먼저 구하는 것으로 바뀌게 되는데 이는 <span style="background-color:#fffacd">**원래의 문제를 작은 두 개의 문제로 바꾸어 푸는 방식**</span>으로 변형시키게 되는 것이다. 작은 두 개의 문제는 아래와 같다.

1) Forward-substitution(전방대치법) - $y$ 구하기

> &#128173; 위에서부터 아래로 가면서 선형식을 풀어 나갈 수 있다.

2) Back-substitution(후방대치법) - $X$ 구하기

> &#128173; 아래에서부터 위로 가면서 선형식을 풀어 나갈 수 있다.

<br/>

#### LU decomposition 의미

LU 분해는 가우스 소거법의 `forward elimination` 을 행렬로 코드화한 것이다.

- L : 행렬 A 를 전방소거하는데 쓰인 replacement 와 scaling 에 대한 EROs 를 기록해 둔 행렬이다.
- U : 행렬 A 를 전방소거한 후 남은 upper triangular matrix  이다.
- P : 행렬 A 를 전방소거하는데 쓰인 interchange 에 대한 EROs 를 기록해 둔 행렬이다.

&#128073; 즉,<code>A = PLU​</code>형태로 리턴을 하게 된다.

<br/>

#### LU decomposition 활용

- 수치적 안정성: 선형시스템 <code>AX = b​</code> 의 해를 역행렬 $A^{-1}$​ 를 이용해 직접 구하는 것 보다 

  <code>PLU</code> 분해를 이용하는 것이 더 수치적으로 안정적이다.

- $b$ 가 자주 업데이트되는 경우: 선형시스템 <code>AX = b​</code> 에서 행렬 $A$ 는 고정되어 있고 $b$ 가 자주 변하는 문제가 종종 있다. 이런 경우, 행렬 $A$ 를 미리 <code>PLU​</code> 로 분해해 둔다면, $b$ 가 업데이트될 때마다 선형시스템의 해 <code>X​</code> 를 실시간으로 구할 수 있다.

<br/>

<br/>

<br/>

### &#128204; QR 분해: $A = QR$, 주어진 행렬에서 정규직교행렬 추출

QR 분해를 설명하기 전에 필요한 몇 가지 개념에 대해 먼저 말하고자 한다.

<br/>

#### 투영 (projection)

두 벡터 $u, a$ 가 있을 때, <span style="background-color:#fffacd">**벡터 $u$ 를 $a$ 위에 투영한 벡터**</span>를 $proj_au$ 라 하고 다음과 같이 구한다.

<br/>
$$
proj_au = (\frac{u\cdot a}{\Vert a \Vert})(\frac{1}{\Vert a \Vert}\mathbf{a}) = (\frac{u \cdot a}{\Vert a\Vert^2})\mathbf{a}
$$

$$
(길이)(방향 )=(기저 \, a에\, 대한\,\, 좌표값)\mathbf{a}
$$

> &#128173; 기저 a 에 대한 좌표값 = scaling 과 같은 개념이다.

- 벡터 $u$ 를 $a$ 위에 투영하고 남은 보완 벡터 (complement vector) 는 $u - proj_au$ 이다.

- projection 과 complement vector 는 서로 <span style="background-color:#fffacd">**직교**</span>하는 성질을 가지고 있다.

<br/>

두 벡터 $u,a$ 가 있을 때, 투영과 보완의 개념을 이용해 <span style="background-color:#fffacd">**직교분할**</span>할 수 있다.

<br/>
$$
proj_au \:\bot \: (u -proj_au)
$$

$$
u = proj_au+(u- proj_au)
$$

- projection 된 벡터와 complement vector 는 서로 직교한다.
- projection 벡터와 complement vector 를 서로 더하면 원래 벡터와 같다.

<br/>

#### 직교행렬(Orthogonal Matrix): 직교좌표계에 대한 행렬 표현

##### **행렬**

행렬은 각 열벡터가 기저 (basis) 를 이루는 **좌표계 (coordinate system)** 이다.

##### **직교행렬 (Orthogonal Matrix)**

주어진 행렬의 모든 열벡터가 서로 직교한다면, 이 행렬을 **직교행렬**이라 한다.

직교행렬은 **직교좌표계**를 의미한다.

<br/>
$$
\left[
\begin{matrix}
    1 & 4 \\
    -2 & 2 \\
\end{matrix}
\right] \quad \quad \left[
\begin{matrix}
    2 & 2 & -4 \\
    2 & 1 & 7\\  6 & -1 & -1
\end{matrix}
\right]
$$
<br/>

> &#128173; 각 열벡터들의 내적이 0 일 경우 서로 직교한다 라고 한다.

<br/>

##### 정규직교행렬 (orthonormal matrix)

주어진 행렬이 **직교행렬**이고 모든 열벡터의 **크기가 1** 이라면 이 행렬을 **정규직교행렬**이라 한다.

정규직교행렬은 **정규직교좌표계**를 의미한다.

<br/>
$$
\left[
\begin{matrix}
    \frac{1}{\sqrt5} & \frac{2}{\sqrt5} \\
    \frac{-2}{\sqrt5} & \frac{1}{\sqrt5} \\
\end{matrix}
\right] \quad \quad \left[
\begin{matrix}
    \frac{1}{\sqrt11} & \frac{2}{\sqrt6} & \frac{-4}{\sqrt66} \\
    \frac{1}{\sqrt11} & \frac{1}{\sqrt6} & \frac{7}{\sqrt66}\\  \frac{3}{\sqrt11} & \frac{-1}{\sqrt6} & \frac{-1}{\sqrt66}
\end{matrix}
\right]
$$
<br/>

#### 직교행렬 (Orthogonal Matrix) 을 이용한 선형시스템

선형시스템 $AX=b$ 에서 행렬 A 가 직교행렬이면, 해 $X$ 는 역행렬 $A^{-1}$ 의 계산없이 

다음과 같이 구할 수 있다.

- $X$ 의 $i$- 번째 요소는 <span style="background-color:#fffacd">**투영 (projection)**</span> 으로 계산할 수 있다.

> &#128173; 즉 벡터 b 를 행렬 A 의 각 열벡터 $a_j$ 에 투영한 연산 $proj_{a_j}b$ 로 부터 
>
> ​       $x_i = \frac { b \cdot a_j} {\Vert a_i \Vert}^2$  (각 축에 대한 스케일 값) 를 계산할 수 있다.

- $X$ 의 $i$- 번째 요소와 $j$- 번째 요소의 계산은 <span style="background-color:#fffacd">**독립적**</span>이다.

> &#128173; 즉 $X$ 의 계산은 병렬처리가 가능하다.

&#128073; 직교가 아니라면 두 벡터 중 하나의 벡터의 방향으로 이동할 때는 다른 벡터의 값이 영향을 

​       미치게 된다.

&#128073; 다만, 직교일 때는 두 벡터 중 어느 하나의 벡터 방향으로 이동하더라도 다른 벡터의 값이 영향을 

​      주지 않는다. 그렇기에 각 벡터별 (축별) 로 따로 계산해도 문제가 없는 것이다.

<br/>

#### 정규직교행렬 (Orthonormal Matrix) 을 이용한 선형시스템

선형시스템 $Ax=b$ 에서 행렬 A 가 정규직교행렬이면, 해 $X$ 는 역행렬 $A^{-1}$ 의 계산없이

다음과 같이 구할 수 있다.

- $X$ 의 $i$- 번째 요소는 <span style="background-color:#fffacd">**내적(inner product)**</span> 으로 계산할 수 있다.

> &#128173; 즉 벡터 b 를 행렬 A 의 각 열벡터 $a_j$ 에 투영한 연산 $proj_{a_i}b$ 로 부터
>
> ​      $x_i = b \cdot a_i$ 임을 계산할 수 있다.

- $X$ 의 $i$- 번째 요소와 $j$- 번째 요소의 계산은 <span style="background-color:#fffacd">**독립적**</span>이다.

> &#128173; 즉 $X$ 의 계산은 병렬처리가 가능하다.

- 정규직교행렬은 <span style="background-color:#fffacd">**회전행렬**</span>이라고도 한다.

> &#128173; $x,y$ 축을 살짝 돌려놓은 것과 비슷한 모양을 보이기 때문이다.

<br/>

### QR 분해: A = QR, 주어진 행렬에서 정규직교행렬 추출

주어진 행렬의 각각의 열벡터들은 직교성이 없지만, 강제로 직교성을 부여해서

직교성을 가진 행렬과 남은 행렬로 분해시키는 것을 말한다.

&#128073; 즉 QR decomposition 는 주어진 행렬을 아래의 형태를 가지는 두 행렬의 곱으로 나누는 

​      행렬분해이다.

<br/>
$$
\quad \quad \quad A \quad \quad \quad=  \quad \quad    Q \quad \quad \quad \quad R
$$
<br/>
$$
\left[
\begin{matrix}
    * & * & * \\
    * & * & *\\  * & * & *
\end{matrix}
\right]  = \left[
\begin{matrix}
    * & * & * \\
    * & * & *\\  * & * & *
\end{matrix}
\right]  \quad \left[
\begin{matrix}
    * & * & * \\
    0 & * & *\\  0 & 0 & *
\end{matrix}
\right]
$$
<br/>

- Q : orthonormal matrix (정규직교행렬)
  - 각각의 열벡터들의 길이는 1 이다.
  - 각각의 열벡터들은 서로 직교한다. (내적이 0 이다.)
- U : upper triangular matrix (상삼각행렬)

<br/>

#### 주어진 행렬 A 가 QR 분해되어 있을 경우 장점

QR 분해를 이용해 $A\mathbf{x} =b $ 문제를 아래와 같이 나타내면

<br/>
$$
A\mathbf{x} = b \Rightarrow (QR)\mathbf{x} = b \Rightarrow Q(R\mathbf{x}) = b \Rightarrow Q \mathbf{y} = b, (단, R \mathbf{x} = \mathbf{y)}
$$
<br/>

선형시스템을 다음과 같이 두 단계로 간단히 해결할 수 있게 된다.

<br/>

1) Inner product (내적): $y$ 구하기

<br/>

​                                                                    $Q$                   $y$       $=$    $b$ 

<br/>
$$
\left[
\begin{matrix}
    * & * & * \\
    * & * & *\\  * & * & *
\end{matrix}\right]   \quad \left[
\begin{matrix}
    y_1  \\
    .. \\ .. \\ y_n
\end{matrix}\right]  = \left[
\begin{matrix}
    *  \\
    * \\  *
\end{matrix}\right]
$$
<br/>

- Q 행렬에서의 각 column vector 들을 b 와 내적한 값이 y 에 값이다.
- 순서를 지킬 필요가 없기에 병렬처리를 통해 y 를 한번에 구해낼 수 있다.

2) Back-substitution (후방대치법): $\mathbf{x}$ 구하기

<br/>

​                                                                   $R$                   $\mathbf{x}$      $=$      $y$       

<br/>
$$
\left[
\begin{matrix}
    * & * & * \\
    0 & * & *\\  0 & 0 & *
\end{matrix}
\right]  \quad  \left[
\begin{matrix}
    x_1  \\
    .. \\ .. \\ x_n
\end{matrix}\right] = \left[
\begin{matrix}
    y_1  \\
    .. \\ .. \\ y_n
\end{matrix}\right]
$$
<br/>

- 최종 $\mathbf{x}$ 값 구하기

<br/>

#### QR decomposition 의 의미

- Q : 행렬 A 에서 정규직교성을 추출한 행렬
- R : 행렬 A 에서 정규직교성 추출 후 남은 upper triangular matrix

> &#128173; QR 분해는 주어진 행렬에서 정규직교성을 추출하여 계산의 편의를 도모한다.

<br/>

#### QR decomposition 의 활용

- 빠른계산: 선형시스템 $A\mathbf{x} = b$ 의 해를 구할 때, 정규직교행렬 Q 를 이용한 계산 부분은

  병렬처리로 빨리 계산할 수 있다. 그러나 R 를 이용한 계산 부분은 병렬처리 할 수 없다.

- $b$ 가 자주 업데이트되는 경우: 선형시스템 $A \mathbf{x}=b$ 에서 행렬 A 는 고정되어 있고 $b$ 가 

  자주 변하는 문제가 종종 있다.이런 경우, 행렬 A 를 미리 QR 분해 한다면, $b$ 가 업데이트될 

  때 마다 선형시스템의 해 $\mathbf{x} $ 를 실시간으로 구할 수 있다.

<br/>

<br/>

### &#128204; QR 분해 vs LU 분해

- <span style="background-color:#fffacd">**LU 분해**</span>의 경우, 선형시스템을 풀 때 <span style="background-color:#fffacd">**병렬처리 할 수 없다.**</span>

> &#128173; LU 분해는 L 을 이용하는 경우도 순서대로 처리해야 하고, U 도 순서대로 처리를 해야하기 
>
> ​      때문에 병렬처리가 불가하다.

- <span style="background-color:#fffacd">**QR 분해**</span>의 경우, Q 행렬이 꽉찬 구조를 가진 행렬이므로 <span style="background-color:#fffacd">**메모리 사용량이 많다.**</span>

> &#128173; Q 가 orthnormal 하기에 꽉찬 구조를 가지게 된다.

<br/>

<br/>

<br/>

### &#128204;  SVD, PCA

#### 특이값 분해 (SVD, Singular Value Decomposition)

LU 분해와 QR 분해는 <code>n x n​ 정방행렬 (square matrix)</code> 에 대한 행렬분해인 반면,

특이값 분해는 일반적인 <code>m x n​ 행렬</code>에 관한 행렬 분해이다.

특히 특이값 분해는 직교분할, 확대축소, 차원변환 등과 관련이 있다.

&#128073; 특이값 분해는 주어진 행렬을 아래의 형태를 가지는 세 행렬의 곱으로 나누는 행렬분해이다.

<br/>
$$
A_{m \times n} = U_{m \times m} \quad D_{m\times n} \quad V^T_{n \times n}
$$

$$
\left[
\begin{matrix}
    *&*&*  \\
    *&*&* \\
    *&*&*
    \\ *&*&*
\end{matrix} \right] = \left[
\begin{matrix}
    *&*&*&*  \\
    *&*&* &*\\
    *&*&*&* \\
    *&*&*&*
\end{matrix} \right] \quad \left[
\begin{matrix}
    *  \\
    &*\\
    &&* \\
   &
\end{matrix} \right]\quad \left[
\begin{matrix}
    *&*&*  \\
    *&*&* \\
    *&*&* 
\end{matrix} \right] 
$$

<br/>

행렬 U, D, T 는 그 특성에 따라 다음과 같은 의미가 있다.

- U : <code>m​</code> 차원 회전행렬 (정규직교행렬)

> &#128173; 각각의 column vector 들이 서로 직교하고 길이가 1인 정규직교행렬의 형태를 띈다.
>
> ​	  또한 회전행렬의 의미를 띄고 있다.

- D : <code>n</code> 차원 확대축소 (확대축소 크기에 따른 정렬 형태) 한 후, <code>n >> m​</code> 으로 차원변환

> &#128173; 축 방향으로 값을 확대하거나 축소하는 의미를 가지고 있다.

- V : <code>n​</code> 차원 회전행렬 (정규직교행렬)

> &#128173; $n \times n$ 정방행렬인 V 의 row vector 들은 축 방향을 가지게 되는 행렬이 나오게 되어 일종의 
>
> ​      회전행렬의 의미가 된다.

&#128073; 1. 회전행렬을 하고 $\rightarrow$ 2. 각 축에 확대축소를 진행하고 $\rightarrow$ 3. 한번 더 회전행렬을 하는 순서로 

​       진행이 된다.

<br/>

예시)

<br/>
$$
A_{3 \times 2} = U_{3 \times 3} \quad D_{3\times 2} \quad V^T_{2 \times 2}
$$

$$
\left[
\begin{matrix}
    2&2  \\
    -\frac{1}{2} & \frac{1}{2} \\
    -2 & -2
    \\ 
\end{matrix} \right] = \left[
\begin{matrix}
    \frac{1}{\sqrt2}&0&\frac{1}{\sqrt2}  \\
    0&1&0\\
    -\frac{1}{\sqrt2}&0&\frac{1}{\sqrt2}
\end{matrix} \right] \quad \left[
\begin{matrix}
    4  \\
    &\frac{1}{\sqrt2}\\
    & \\
\end{matrix} \right]\quad \left[
\begin{matrix}
    \frac{1}{\sqrt2}&\frac{1}{\sqrt2}  \\
    -\frac{1}{\sqrt2}&\frac{1}{\sqrt2}  
\end{matrix} \right]
$$

<br/>

1. 2차원 입력에 대해 V 행렬을 통해 전체적인 입력을 회전시킨다.

2. 회전된 형태에서의 값을 행렬 D 를 통해 증폭시키게 된다.

3. 마지막으로 행렬 U 의 값으로 각 축에 대하여 회전시킨다.

<br/>

#### 특이값 분해 (SVD) 의 활용

- A 의 특이값 분해 $U, D, V$ 는 각각 열벡터의 순서대로 행렬 A 의 열벡터가 어떤 방향으로 

  강한 응집성을 보이고 있는지를 분석하는 것이다.

- $U,D,V$ 의 열벡터를 순서대로 $p$ 개 취한다면, 강한 응집성을 가지는 $p$ 개의 방향으로

  수선의 발을 내린 A 의 근사치 A' 를 재구성할 수 있다.



예) 증폭값이 가장 큰 경우만 취할 경우

<br/>
$$
A_{3 \times 2} = U'_{3 \times 1} \quad D'_{1\times 1} \quad V'^T_{1 \times 2} = A'_{3 \times 2}
$$

$$
\left[
\begin{matrix}
    2&2  \\
    -\frac{1}{2} & \frac{1}{2} \\
    -2 & -2
    \\ 
\end{matrix} \right] = \left[
\begin{matrix}
    \frac{1}{\sqrt2}  \\
    0\\
    -\frac{1}{\sqrt2}
\end{matrix} \right] \quad \left[
\begin{matrix}
    4  \\
 
\end{matrix} \right]\quad \left[
\begin{matrix}
    \frac{1}{\sqrt2}&\frac{1}{\sqrt2}  \\
     
\end{matrix} \right] = \left[
\begin{matrix}
    2&2  \\
    0 & 0 \\
    -2 & -2
    \\ 
\end{matrix} \right]
$$

<br/>

> &#128173; 응집성이 높다라는 것은 해당 방향으로 길이가 길게 늘어뜨러져 있는 것을 의미한다. 
>
> &#128173; 응집성이 높은 경우만을 계산하면 근사치로 계산이 되는데 이 값은 원래의 값과 같
>
> ​       은 차원을 가진다.
>
> &#128173; 다만, 응집성이 높은 정보만이 살아 있고 상대적으로 응집성이 낮은 경우는 정보가 손  
>
> ​      실되는 결과를 가져온다. 이는 일종의 정보축약을 시키는 것이라 볼 수 있다.

&#128073;  데이터의 응집성이 높은 방향만 선택적으로 취하는 방식이다. 특히 영상처리에서 많이 쓰인다.



<br/>

<br/>

<br/>

### &#128204; 주성분 분석 (Principal Component Analysis, PCA)

주성분분석 (PCA) 는 데이터의 공분산행렬 (covariance matrix) 에 대한 고유값 분해에 기반을 둔

직교분해이다.

$K$ 개의 $n$ 차원 데이터 $\{\mathbf{x}_i\}^K_{i=1}$ 가 있을 때, 데이터의 중심 $m$ 과 공분산행렬 $C$ 는 다음과 같이 구할 수 있다.<br/>
$$
m = \frac{1}{K} \sum_{i=1}^{K}\mathbf{x}_i, C =\frac{1}{K} \sum_{i=1}^{K}(\mathbf{x}_i - m) (\mathbf{x}_i - m)^T
$$
<br/>

1. 우선 데이터의 중심 $m$ 을 먼저 구한다.
2. 각 데이터와 $m$ 간의 외적을 구한다.
3. 해당 값들의 평균이 공분산행렬 $C$ 가 된다.

<br/>

공분산행렬 $C$ 에 대해 주성분분석(PCA) 은 아래와 같다.

<br/>
$$
C_{n \times n} = W_{n \times n} \quad D_{n\times n} \quad W^T_{n \times n} 
$$

$$
\left[
\begin{matrix}
    *&*&*  \\
    *&*&* \\
    *&*&*

\end{matrix} \right] = \left[
\begin{matrix}
    *&*&* \\
    *&*&* \\
    *&*&* \\
 
\end{matrix} \right] \quad \left[
\begin{matrix}
    \lambda_1  \\
    &..\\
    && \lambda_n\\
   
\end{matrix} \right]\quad \left[
\begin{matrix}
    *&*&*  \\
    *&*&* \\
    *&*&* 
\end{matrix} \right] 
$$

<br/>

- W : $n$ 차원 회전행렬(정규직교행렬) 

> &#128173; 열방향으로 데이터가 나열되어 있다.

- D : $n$ 차원 확대축소 (확대축소 크기에 따른 정렬형태)

> &#128173; 일종의 증폭값의 의미이다.
>
> &#128173;  $\lambda$ 가 크면 그 방향으로 데이터 응집성이 큰 경우이다.

<br/>

<br/>

<br/>

### &#128161; Check Point

- 행렬분해는 다음과 같은 3가지가 있다.

  - LU decomposition
  - QR decomposition
  - SVD

- LU, QR decomposition 은 <code>n x n 정방행렬 (square matrix)</code> 에 대한 행렬분해이고 

  SVD 는 <code>m x n​ 행렬</code> 에 대한 행렬분해이다.

- SVD 와 PCA 는 데이터 응집성이 큰 방향에 영향이 크다.