---
title: "[Programmers Dev] 가우스 소거법 "
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

## &#128161; 가우스 소거법

역행렬을 구하기 위한 알고리즘으로 자주 쓰이는 방법이다.



### 선형시스템의 해 (Solutions of a Linear System)

1) 해가 하나인 경우 (unique solution)

<br/>
$$
\left[
\begin{matrix}
1 & 3 \\
-2 & 1 \\
\end{matrix}
\right
]  \left[
\begin{matrix}
x_1 \\
x_2 \\
\end{matrix}
\right
] = \left[
\begin{matrix}
2 \\
3 \\
\end{matrix}
\right
]
$$
<br/>

2) 해가 없는 경우 (no solution)

<br/>
$$
\left[
\begin{matrix}
1 & 3 \\
2 & 6 \\
\end{matrix}
\right
] 
\left[
\begin{matrix}
x_1 \\
x_2 \\
\end{matrix}
\right
] = \left[
\begin{matrix}
2 \\
5 \\
\end{matrix}
\right
]
$$

> &#128173; 역행렬을 가지지 않는 행렬을 `singular 하다` 라고 함



3) 해가 여러개인 경우 (infinitely many solutions)

<br/>
$$
\left[
\begin{matrix}
1 & 3 \\
2 & 6\\
\end{matrix}
\right
]\left[
\begin{matrix}
x_1 \\
x_2 \\
\end{matrix}
\right
] = \left[
\begin{matrix}
2 \\
4 \\
\end{matrix}
\right
]
$$
<br/>

<br/>

### Gauss elimination (가우스 소거법)

: Gauss elimination 은 임의의 $m$ x $n$ 선형시스템의 해를 구하는 가장 대표적인 방법이다.

Gauss elimination 은 다음의 두 단계로 수행된다.

1. Forward elimination (전방소거법): 주어진 선형시스템을 아래로 갈수록 더 단순한 형태의 선형방정식을 가지도록 변형한다.
2. Back - substitution (후방대입법): 아래에서부터 위로 미지수를 실제값으로 대체한다.

> &#128173; 두 가지중 Forward elimination 이 중요!!

<br/>

<br/>

#### 1) Forward Elimination (전방소거법)

다음과 같이 forward elimination 은 주어진 선형시스템을 아래로 갈수록 더 단순한 형태의 선형방정식을 가지도록 변형하는 절차

<br/>

주어진 선형시스템

<br/>
$$
\left[
\begin{matrix}
1 & 2&1 \\
1&2&3 \\
2&3&-1
\end{matrix}
\right
]\left[
\begin{matrix}
x_1 \\
x_2 \\
x_3 \\
\end{matrix}
\right
] = \left[
\begin{matrix}
1 \\
3 \\
-3
\end{matrix}
\right
]
$$
<br/>

Forward elimination 수행 후

<br/>
$$
\left[
\begin{matrix}
1 & 2&1 \\
0&1&3 \\
0&0&1
\end{matrix}
\right
]\left[
\begin{matrix}
x_1 \\
x_2 \\
x_3 \\
\end{matrix}
\right
] = \left[
\begin{matrix}
1 \\
5 \\
1
\end{matrix}
\right
]
$$

> &#128173; forward: 위에서부터 아래로 가는 것 혹은 왼쪽에서 오른쪽으로 가는 방향을 말함
>
> &#128173; forward 로 불리는 모든 방향에 대해서 0 을 최대한 많이 배치하는 것이 중점

&#128073; 1. 아래로 가면서 2. 오른쪽으로 가면서 0 을 많이 만들어 행렬의 모양이 역삼각형 모양처럼 만들어 나가며 **<span style="background-color:#fffacd">제일 마지막 줄을 가장 단순한 선형방정식</span>**으로 만들어 나가는 절차이다.

<br/>

#### 2) Back - substitution (후방대입법)

아래에서부터 위로 미지수를 실제값으로 대체하여 선형시스템의 해 (solution) 를 구하는 절차

<br/>

Forward elimination 수행 후

<br/>
$$
\left[
\begin{matrix}
1&2&1 \\
0&1&3 \\
0&0&1
\end{matrix}
\right
] = \left[
\begin{matrix}
x_1 \\
x_2 \\
x_3
\end{matrix}
\right
] = \left[
\begin{matrix}
1 \\
5 \\
1
\end{matrix}
\right
]
$$
<br/>

Back - substitution 수행 후

<br/>
$$
\left[
\begin{matrix}
1&2&1 \\
0&1&3 \\
0&0&1
\end{matrix}
\right
]\left[
\begin{matrix}
-4 \\
-2\\
 1
\end{matrix}
\right
] = \left[
\begin{matrix}
1 \\
5 \\
1
\end{matrix}
\right
]
$$

> &#128173; 이 때, 아래에서부터 위로 풀어나가는 각 선형방정식은 가장 단순한 형태이다.

&#128073; 즉, 위와같은 절차는 문제를풀어나갈 수 있도록 **<span style="background-color:#fffacd">선형시스템을 변형해 나가는 절차</span>**이다.

<br/>

[연습문제]

<br/>
$$
\left[
\begin{matrix}
1 & 2 &1 \\
1 & 2 & 3 \\
2 & 3 & -1
\end{matrix}
\right
] \left[
\begin{matrix}
x_1 \\
x_2 \\
x_3
\end{matrix}
\right
] = \left[
\begin{matrix}
1 \\
3 \\
-3
\end{matrix}
\right
]
$$
<br/>

$E1: x1 + 2x2 + x3 = 1$

$E2: x1 + 2x2 + 3x3 = 3$

$E3: 2x1 + 3x2-x3=-3$

<br/>

**&#128204; Gauss elimination 의 절차**

> $E1$ 의 $x1$ 의 계수를 1 로 만들고 밑에 있는 변수들을 제거하는 것이 1차목표
>
> &#128173; 1 행 1 열을 기준(pivot) 으로 잡기

- 2 번째 행의 첫 번째 열인 1 을 0 으로 만들도록 변형

- $E2 = E2 - E1$ 로 update

$$
\left[
\begin{matrix}
1 & 2 &1 \\
0 & 0 & 2 \\
2 & 3 & -1
\end{matrix}
\right
] \left[
\begin{matrix}
x_1 \\
x_2 \\
x_3
\end{matrix}
\right
] = \left[
\begin{matrix}
1 \\
2 \\
-3
\end{matrix}
\right
]
$$

<br/>

- 남아 있는 3 번째 행의 첫 번째 열인 2 를 0 으로 만들도록 변형
- $E3 = E3 - 2E1$ 로 update

$$
\left[
\begin{matrix}
1 & 2 &1 \\
0 & 0 & 2 \\
0 & -1 & -3
\end{matrix}
\right
] \left[
\begin{matrix}
x_1 \\
x_2 \\
x_3
\end{matrix}
\right
] = \left[
\begin{matrix}
1 \\
3 \\
-5
\end{matrix}
\right
]
$$

<br/>

> E2 의 $x2$ 의 계수를 1 로 만들고 밑에 있는 변수들을 제거하는 것이 2차 목표
>
> &#128173; 2 행 2 열을 기준(pivot) 으로 잡기

- 현재 계수가 이미 0 이기에 2 번째 행과 3 번째 행의 위치를 바꿈
- $E2, E3 = E3, E2$

$$
\left[
\begin{matrix}
1 & 2 &1 \\
0 & -1 & -3 \\
0 & 0 & 2
\end{matrix}
\right
] \left[
\begin{matrix}
x_1 \\
x_2 \\
x_3
\end{matrix}
\right
] = \left[
\begin{matrix}
1 \\
-5 \\
2
\end{matrix}
\right
]
$$

<br/>

> E2 의 $x2$ 의 계수를 1로 만듬

- $E2 = -E2$

$$
\left[
\begin{matrix}
1 & 2 &1 \\
0 & 1 & 3 \\
0 & 0 & 2
\end{matrix}
\right
] \left[
\begin{matrix}
x_1 \\
x_2 \\
x_3
\end{matrix}
\right
] = \left[
\begin{matrix}
1 \\
5 \\
2
\end{matrix}
\right
]
$$



<br/>

> 다음으로 $E3$ 의 $x3$ 의 계수를 1로 만드는 것이 3차 목표
>
> &#128173; 3 행 3 열을 기준(pivot) 으로 잡기

- $E3 = 0.5*E3$

$$
\left[
\begin{matrix}
1 & 2 &1 \\
0 & 1 & 3 \\
0 & 0 & 1
\end{matrix}
\right
] \left[
\begin{matrix}
x_1 \\
x_2 \\
x_3
\end{matrix}
\right
] = \left[
\begin{matrix}
1 \\
5 \\
1
\end{matrix}
\right
]
$$

> Forward elimination 절차가 끝났으므로 Back-substitution 을 수행 후 X 를 구하면 됨

<br/>

#### 소거법에 쓰이는 Elementray Row Operations (EROs, 기본행연산)

- Replacement(치환): $r_j = r_j - m*r_j$
  - $j$ 번째 행을 기준 행인 $i$ 번째 행을 $m$ 배하고 빼서 업데이트 한다.
- Interchange(교환): $r_i, r_j = r_j, r_i$
  - $j$ 번째 행과 $i$ 번째 행의 위치를 서로 바꾼다.
- Scaling(스케일링): $r_j = s*r_j$
  - $j$ 번째 행을 $s$ 배 스케일링한다.

<br/>

#### Upper triangular form (상삼각형태)

Forward elimination 은 EROs 을 활용하여 주어진 선형시스템 $Ax=b$ 에서 행렬 $A$ 를

upper triangular form 으로 만드는 작업을 수행한다.

<br/>

#### Rank

의미 있는 식의 개수

> &#128173; $0x=0$ 라는 의미 없는 식을 제외한 나머지 식의 개수를 의미한다.
>
> &#128173; forward elimination 을 진행하면 의미 없는 식은 모든 항이 0 으로 바뀌게 되므로
>
> ​      rank 의 값을 알 수 있다.

<br/>

### &#128161; Check Point

- forward elimination 은 주어진 선형시스템을 <span style="background-color:#fffacd">**가장 풀기 쉬운 꼴**</span>로 변형해 준다.
- forward elimination 은 주어진 선형시스템의**<span style="background-color:#fffacd"> rank</span>** 를 알려준다.
- forward elimination 은 선형시스템이 해가 있는지 (consistent) 아니면 해가 없는지 (inconsistent) 알려준다.