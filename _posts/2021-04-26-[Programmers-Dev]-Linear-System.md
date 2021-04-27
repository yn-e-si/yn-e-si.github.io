---
title: "[Programmers Dev] 선형시스템 (Linear System) "
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

## &#128161; 선형시스템 (Linear System)

- 가장 간단한 형태의 `linear system` 

$3x = 6$ 

<br/>

- 연립일차방정식의 대수적 표현: $AX = b$

$3x + y = 2, x - 2y = 3$

$3x + y + z = 4, x -2y - z =1, x +y + z = 2$

<br/>

<br/>

#### &#128204; 선형대수 (Linear Algebra) 의 목표

선형대수 (linear algebra) 의 목표는 어떤 연립일차방정식, 즉 <span style="background-color:#fffacd">**linear system** 문제라도 **정형적인 방법으로 표현하고 해결하는 방법**을 배우는 것</span> 이다.

ex.

$AX = b$

$A^{-1}AX = A^{-1}b$

$X = A^{-1}b$

&#128073; 이와 같이 복잡한 시스템이라도 $AX = b$ 로 표현 가능하고 푸는 방식도 쉽게 할 수 있다

<br/>

<br/>

#### Linear System (선형시스템) 의 구성요소: Linear Equations (선형방정식)

- $3x+y+z =4$
- $x-2y-z=1$
- $x+y+z=2$

> &#128173; 이 방정식들을 각각 linear equation (선형방정식) 이라한다.
>
> &#128173; linear: 평면이나 왜곡되지 않은 올바른 공간처럼 올곧은 형태를 의미한다.

&#128073;  방정식이 이처럼 올곧은 공간처럼 형성된다면 **<span style="background-color:#fffacd">linear equations</span>** 이라고 말한다.

&#128073; 선형방정식이 가지고 있는 미지수를 각각 **<span style="background-color:#fffacd">unknown (혹은 variable)</span>** 이라 한다.

&#128073; 모든 방정식을 만족하는 변수들을 구하는 것을 **<span style="background-color:#fffacd">선형시스템을 푼다</span>** 라고 한다

<br/>

<br/>

#### $m$ x $n$ Linear System (선형시스템)

**$m$** 개의 linear equations 과 **$n$** 개의 unknowns 로 구성된 **선형시스템**을 말한다.

- $3x + y + z =4$
- $x-2y-z =1$
- $x+y+z=2$

> &#128173; 위의 선형시스템을 <code>3 x 3 linear system</code> 이라 한다.

- $3x+y+z=4$
- $x-2y-z=1$

> &#128173; 위의 선형시스템을<code>2 x 3 linear system</code> 이라 한다.

- $2x+y=3$

> &#128173; 위의 방정식을 <code>linear equation</code> 이라 한다.

- $sinx + y =2$
- $3x+y^3 = 2$

> &#128173; 위의 방정식 각각을 <code>non-linear equation</code> 이라 한다.

&#128073; 위의 예시와 같이 미지수의 승수가 **1승**으로만 구성되어 있다면 이는 **<span style="background-color:#fffacd">선형적인 형태</span>**이다.

&#128073; **<span style="background-color:#fffacd">linear system </span>** 을 구성하는 각각의 식들은 항상 **<span style="background-color:#fffacd">linear equations</span>** 이여야 한다.

<br/>

<br/>

#### Linear System (선형시스템) 의 대수적 표현: $AX=b$

> **$AX=b$ 로 표현하기**

1. 선형시스템의 unknowns 를 모아 column vector <code>$X$</code> 로 표현한다.
2. 선형시스템의 linear equation 에 대해 다음을 수행한다.
   - <code>coefficients</code> 를 모아 A 의 row vector 로 표현
   - <code>constant</code> 를 모아 b 에 표현

$$
\left[
\begin{matrix}
1 & 2 \\
3 & 4 \\
\end{matrix}
\right
] \left[
\begin{matrix}
x \\
y \\
\end{matrix}
\right
]  = \left[
\begin{matrix}
2 \\
3  \\
6 \\
\end{matrix}
\right
] 
$$

$$
A X = b
$$

> &#128173; 위의 형태를 <code>3 X 5 linear system</code>이라 한다.

<br/>

<br/>

### &#128161; Check Point

$m*n$ 선형시스템: $AX=b$

- 각각의 식은 행으로 표현되기에 matrix 에서의 행은 식을 의미한다. (linear equation = row) 
- $m$ 은 linear equation 의 개수이다.
- $n$ 은 unknown 의 개수이다.
- $A$ 는 $m$ x $n$ 행렬이다.
- $X$ 는 $n$- 벡터이다.
- $b$ 는 $m$- 벡터이다.



