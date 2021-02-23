---
title: "[Google Bootcamp] 1. Neural Networks and Deep Learning"
excerpt: "Week2: Neural Networks Basics"
categories:
 - DL
tags:
 - Google Bootcamp
 - Coursera
 - Deep Learning
---

이 포스팅은 *[Google Machine Learning Bootcamp]* 중 *[Coursera - Deep Learning Specialization Course by Andrew Ng]*의 *review*를 위해 작성된 포스팅 입니다.

![](https://yn-e-si.com/assets/images/1-2/1.JPG){: .align-center}

위의 고양이 image가 64 * 64 를 갖는 image라고 가정한다면

해당 image의 차원은 64*64*3 이다.

이 image가 실제 프로그램상에서는 $X$와 같이 표기된 형태로 들어간다고 생각하면 된다.

이렇게 64*64*3 인 차원을 12288로 바꾸는 것을 *Flatten한다*  라고하는데

이 값이 해당 image의 차원의 수라고 생각하면 된다.

또한 이 차원 그대로 input이 되는 것이고 Binary Classification이라고 생각한다면 $y$ {0,1} 중에

하나의 값만을 가지게 된다.

![](https://yn-e-si.com/assets/images/1-2/2.JPG){: .align-center}

$(x,y)$는 input 과 output의 순서쌍이라고 생각하면 된다.

이 때,

$x$가 갖는 차원의 수 = $n_x$

training sample의 수 = $m$

이라고 표기하기로 약속한다.

즉, $X$는 위와 같이 **n개의 차원을 갖는 m개의 데이터**로 되어있고

$Y$는 **1개의 차원을 갖는 m개의 데이터**로 이루어져 있는 것이다.

![](https://yn-e-si.com/assets/images/1-2/3.JPG){: .align-center}

위의 사진은 이 후 강의에서 쓰이게 될 용어에 대해 정리한 것이다.

### 다음으로 Logistic Regression에 대한 설명이다.

![](https://yn-e-si.com/assets/images/1-2/4.JPG){: .align-center}

우선, Logistic Regression은 Binary classfication에서 쓰이는 알고리즘이다.

이 알고리즘은 주어진 $x$를 통하여 output인 $\hat{y}$를 얻는 것인데

$\hat{y}$같은 경우 binary 이기에 0~1사이에 확률값은 가지게 된다. → $P( y=1 | x)$

다만, Logistic Regression은 $\hat{y}$값이 0~1사이에 값을 가지게 하기엔 확률상으로 어려움이 많기에

그다지 좋은 알고리즘은 아니다.

또한 Logistic Regression은 시그모이드 함수를 이용하는데 이는 위에 보이는 그래프와 같다.

마지막으로, Logistic Regression은 $w$ 와 $a$ 로 이루어진 파라미터 $Z$에 대하여

$$\hat{y} = \sigma(w^tx + b)$$

$$z = w^tx + b$$

$$\sigma(z) = \frac{1}{  1+e^{-z}}$$

로 정의될 수 있다.

이는 $Z$값이 커지면 커질수록 1에 가까워지고, $Z$값이 작으면 작아질수록 0에 가까워진다.

→ **즉, Logistic Regression을 사용할 때의 핵심은 parameter: $w$와 $b$를 조정하여 $\hat{y}$이 $y=1$이 되는 확률을  잘 추정한 수치가 나올 수 있도록 하는 것.**

### Logistic Regression의 parameter - $w$와 $b$를 정의하기 위한 Cost function에 대한 내용이다.

![](https://yn-e-si.com/assets/images/1-2/5.JPG){: .align-center}

- $i$는 $i$ - th example를 의미 한다.
- L(Loss function)이 의미하는 것은 true label $y$를 갖을 때, 얼마나 정확히 $\hat{y}$을 산출하는지 이다.
- 제곱을 사용하여 L을 정의할 경우 gradient descent가 잘 나오지 않는다는 단점이 있기에 제곱으로 사용하지 않는다.
- gradient descent가 잘 나오지 않는다면 optimization하는데 어려움이 생기게 된다.
- L의 목표는 값을 최대한 작게 만드는 것이다.

Logistic Regression loss function

$$L(\hat{y},y) = -(ylog\hat{y} + (1-y)log(1-\hat{y}))$$

- $y=1$이라면, $L(\hat{y},y) = - log\hat{y}$ 가 된다. 그렇기에 이 값을 최소로 만들기 위해선 $\hat{y}$를

크게 만들어야 한다.

- $ y=0$이라면, $L(\hat{y}-y) = - log(1-\hat{y}) $가 된다. 그렇기에 이 값을 최소로 만들기 위해선 $\hat{y}$를

작게 만들어야 한다.

Logistic Regression Cost Function

— Loss함수가 single training example에 대하여 적용된 것 —

- 최적의 $w,b$ 를 찾고 $J$를 줄이는 것이  cost function의 궁극적인 목표

$$J(w,b) = \frac{1}{m}\Sigma L(\hat{y}^{(i)},y^{(i)}) = -\frac{1}{m}[y^{(i)}log\hat{y}^{(i)}+(1-y^{(i)})log(1-\hat{y}^{(i)})]$$

### Gradient Descent

- J(w,b)를 최소로 갖는 w,b를 찾기 위해선 우선 w,b를 초기화 시켜줘야 함
- 일반적으로 0으로 초기화하거나 random으로 초기화 시킴

![](https://yn-e-si.com/assets/images/1-2/6.JPG){: .align-center}

learning rate(=$ \alpha $): 한번에 얼마만큼 gradient descent를 진행할지 조절해주는 역할

e

$$







derivative: w,b에 얼마나변화를 줄지 알려주는 값(특정 지점에서의 함수의 기울기)

![](https://yn-e-si.com/assets/images/1-2/7.JPG){: .align-center}

- 기울기 값이 음수일 경우, W는 증가
- 기울기 값이 양수일 경우, W는 감소

즉, **Gradient Descent**는 cost function의 parameter인 **초기화된 w,b**에 대해서 cost function의 **derivative값**과 **learning rate**를 통해 감소시켜나아가며 **global minimum**을 찾아가는 과정이다.

### Computation Graph

![](https://yn-e-si.com/assets/images/1-2/8.JPG){: .align-center}

- Computation graph는 파란선과 같이 왼쪽에서 오른쪽으로 계산해가는 과정이다.
- 이와 반대로 오른쪽에서 왼쪽으로 가는 빨간색 과정은 derivative로 볼 수 있다.
- J는 우리가 최소로 만들고 싶은 cost function으로 볼 수 있다.

![](https://yn-e-si.com/assets/images/1-2/9.JPG){: .align-center}

$\frac{dJ}{dv} = dv = 3$ →  v가 변할 때, J에 미치는 영향을 말함

- 즉, v가 변할 때 J는 3배만큼 커진다는 것을 의미

$\frac{dJ}{da} = \frac{dJ}{dv} *\frac{dv}{da} = 3 * 1 = 3$ → a가 변할 때, J에 미치는 영향을 말함

- a값이 변하게 되면 v값이 변하게 되고 v값이 변하면 J값이 변하게 됨
- 즉, chain rule에 의해 a가 J에 미치는 영향을 구할 수 있음

### 표기법

- $\frac{dFinalOutputVar}{dvar}$ → $dvar$ : 최종 output에 관한 derivative의 변수명
- $\frac{dJ}{dv}$  → $dv$ : dv에 관한 derivative의 변수명
- $\frac{dJ}{du}$→ $du$ : du에 관한 derivative의 변수명
- $\frac{dJ}{da}$→ $da$ : da에 관한 derivative의 변수명
- $\frac{dJ}{db}$→ $db$ : db에 관한 derivative의 변수명
- $\frac{dJ}{dc}$→ $dc$ : dc에 관한 derivative의 변수명

![](https://yn-e-si.com/assets/images/1-2/10.JPG){: .align-center}

$\frac{dJ}{du} = \frac{dJ}{dv}*\frac{dv}{du} = 3 * 1 = 3$ → u가 변할 때, J에 미치는 영향을 말함

$\frac{dJ}{db} = \frac{dJ}{du}*\frac{du}{db} = 3 * 2 = 6$ → b가 변할 때, J에 미치는 영향을 말함

$\frac{dJ}{dc}=\frac{dJ}{du}*\frac{du}{dc} = 3*3 = 9$ → c가 변할 때, J에 미치는 영향을 말함

즉,  **cost function의 값**을 계산할 때는, left to right인 **forward** 방식으로 계산

**derivateives**를 계산할 때는, right to left인 **backwards** 방식으로 계산

### Logistic Regression Gradient Descent

![](https://yn-e-si.com/assets/images/1-2/11.JPG){: .align-center}

앞서 언급했던 Logistic regression에 대하여 Computation Graph를 그려보면 위와 같다.

![](https://yn-e-si.com/assets/images/1-2/12.JPG){: .align-center}

이를 통해 backwards방식으로 진행해보면 다음과 같다.

$\frac{dL(a,y)}{da} = -\frac{y}{a} + \frac{1-y}{1-a}$  → $da$

$\frac{dL(a,y)}{dz}=\frac{dL}{da}*\frac{da}{dz} = (-\frac{y}{a} + \frac{1-y}{1-a})  * a(1-a) = a-y$ → $dz$

$\frac{dL}{dw_1} = x_1*dz$ → $dw_1$

$\frac{dL}{dw_2} = x_2*dz$ → $dw_2$

$\frac{dL}{db} = dz$ → $db$

즉, 위에서 구한 값들에 의해 $L(a,y)$에 대한 1개의 example에 대해서

$w_1, w_2, b$는 다음과 같이 update가 된다.

> $w_1 := w_1 - \alpha*dw_1$

> $w_2 := w_2 - \alpha *dw_2$

> $b := b - \alpha * db$

![](https://yn-e-si.com/assets/images/1-2/13.JPG){: .align-center}

- m 개의 examples에 대하여 적용할 때는 위와 같이 전체 값의 평균을 구하면 됨

![](https://yn-e-si.com/assets/images/1-2/14.JPG){: .align-center}

1. **parameter들을 초기화 시켜 줌**

$J=0, dw_1=0, dw_2 =0, db=0$

1. ***m examples\*에 대하여 반복한 뒤 평균을 구해줌**

$dw_1 += X^{(i)}_1 * dz^{(i)}$   → $dw_1 /=m$

$dw_2 += X^{(i)}_2*dz^{(i)}$ → $dw_2/=m$

$db += dz^{(i)}$ → $db/=m$

1. **최종 적용되는  update 값**

$w_1 := w_1 - \alpha * dw_1$

$w_2 := w_2 - \alpha*dw_2$

$b := b - \alpha*db$

### 단, 위와 같은 알고리즘 방식으로 접근 시 2가지 문제가 생김

1. 모든 *m*개의 sample에 대하여 for문이 돌게 되는 문제
2. 모든 *n*에 대하여 for문이 돌게 되는 문제

→ 따라서 **n,m이 커질수록** **시간과 비용**이 많이 들게 되는 문제가 생김

→ 이를 해결하기 위한 방안으로는 **Vectorization**이 있음

### Vectorization

![](https://yn-e-si.com/assets/images/1-2/15.JPG){: .align-center}

Non- vectorized

```python
z=0
for i in range(n-x):
	z += w[i] **[i]
z +=b
```

Vectorized

```python
z = np.dot(w,x) +b
```

- 딥러닝 알고리즘을 적용할 경우, Vectorized를 이용한 것이 더 빠르게 결과값을 얻어 낼 수 있음
- for문을 사용하는 경우 속도가 현저히 느려지기 때문에, 딥러닝 알고리즘에선 되도록 사용을 피해야 함
- np.function과 같은 built-in 기능을 사용하면, python이 paralleslism을 활용할 수 있게 계산을 하게 되어 속도가 더 빨라짐

![](https://yn-e-si.com/assets/images/1-2/16.JPG){: .align-center}

![](https://yn-e-si.com/assets/images/1-2/17.JPG){: .align-center}

- non-vectorized = for loop 과 같은 맥락
- numpy 안에는 많은 함수들이 built-in 되있으므로 최대한 사용하는 것이 좋음

![](https://yn-e-si.com/assets/images/1-2/18.JPG){: .align-center}

Logistic regression derivatives에 사용되고 있는 2개의 for-loop에 대해서 1개를 제거하는 과정

$dw_1 =0, dw_2=0$ → vectorize → $dw = np.zeros((n-x, 1))$

$dw_1 += x^{(i)}_1*dz^{(i)}, dw_2 = x^{(i)}_2*dz^{(i)}$ → vectorize → $dw += x{(i)}*dz^{(i)}$

$dw_1 = dw_1/m, dw_2 = dw_2/m$ → vectorize → $dw /=m$

### Vectorization을 활용하여 for-loop없이 값을 구하는 과정

![](https://yn-e-si.com/assets/images/1-2/19.JPG){: .align-center}

### forward

- $z^{(1)} = w^Tx^{(1)} + b, z^{(2)} = w^Tx^{(2)} + b, ... ,z^{(m)} = w^Tx^{(m)} + b$ 로 되어있는 것을 vector의 형태로 표현
- 즉, $Z=[\ z^{(1)},z^{(2)},...,z^{(m)} \ ] = [\ w^Tx^{(1)}+b, \ w^Tx^{(2)}+b, \ ..., \  w^Tx^{(m)}+b \ ]$ 의 $(1*m)$  matrix 형태
- 이를 활용하여 $A = [ \ a^{(1)},\ a^{(2)},...,\ a^{(m)} \ ] = \sigma^{(z)}$ 로 표현 가능

![](https://yn-e-si.com/assets/images/1-2/20.JPG){: .align-center}

### backward

- $dz^{(1)} = a^{(1)} - y^{(1)}, \ a^{(2)} - y^{(2)}, \ ..., \ a^{(m)} - y^{(m)}$로 되어있는 것을 vector의 형태로 표현
- 즉, $dZ = [ \ dz^{(1)}\ dz^{(2)}\ ... \ dz^{(m)}\ ]  = [ \ a^{(1)}-y^{(1)} \ a^{(2)}-y^{(2)} \ ... \ a^{(m)}-y^{(m)} \ ]$ 의 $(1*m)$ matrix 형태
- 이를 활용하여 $db = \frac{1}{m} * np.sum(dZ), dw= \frac{1}{m}*X*dZ^{T}$로 표현 가능

![](https://yn-e-si.com/assets/images/1-2/21.JPG){: .align-center}

- 좌측에 보이는 코드는 for-loop을 2번 사용하는 비 효율적인 non-vectorize 형식

이를 위의 vectorization을 사용하여 표기하면 다음과 같아짐

$Z=w^TX +b = np.dot(w.T,X) +b$

$A = \sigma(Z)$

$dZ=A-Y$

$dw=\frac{1}{m}*X*dZ^T$

$db = \frac{1}{m}*np.sum(dZ)$

따라서 $w,b$는 각각 한번의 gradient descent를 진행하면 다음과 같이 update가 됨

- $w := w-\alpha * dw$
- $b := b - \alpha * db$

— 참고 —

### Broadcasting

![](https://yn-e-si.com/assets/images/1-2/22.JPG){: .align-center}

![](https://yn-e-si.com/assets/images/1-2/23.JPG){: .align-center}

브로드 캐스팅이 일어날 수 있는 조건

- 차원의 크기가 1일 때 가능

→ 두 배열 간의 연산에서 최소한 하나의 배열의 차원이 1이라면(0번축이든 1번축이든; 1행이든 1열이든) 가능

- 차원의 짝이 맞을 때 가능

→ 차원에 대해 축의 길이가 동일하면 브로드캐스팅이 가능

![](https://yn-e-si.com/assets/images/1-2/24.JPG){: .align-center}

![](https://yn-e-si.com/assets/images/1-2/25.JPG){: .align-center}

shape: (2,3) 인 array에서 axis=1로 계산할 경우 shape은 2

axis = 0 으로 계산할 경우 shape은 3

shape: (4, 3, 2)인 array에서 axis = 0으로 계산할 경우 shape은 (3,2)

axis = 1 → (4,2)

axis = 2 → (4,3)

### Code error 방지 Tips

— rank 1 array vs row,column vector —

- rank 1 array

```python
import numpy as np
a = np.random.randn(5)
-> [ 0.17689476  1.87726456 -1.02728566  0.29455378  1.27477034 ]
a.shape
-> (5,)
a.T
-> [ 0.17689476  1.87726456 -1.02728566  0.29455378  1.27477034 ]
np.dot(a,a.T)
-> 6.322531175757316
```

→ 위와 같이 array를 만들 경우 row vector or column vector도 아닌 rank 1 array 형태로 생성이 됨. 이는 코드 연산 시 error가 발생할 가능성이 높으므로

Don't use!!!

- row,column vector

```python
import numpy as np
a = np.random.randn(5,1) # column vector
->[[-0.85203828]
   [ 0.73566251]
   [-1.70892747]
   [-1.12704725]
   [-0.9160968 ]]
a.shape
-> (5,1)
a.T
-> [[-0.85203828  0.73566251 -1.70892747 -1.12704725 -0.9160968 ]] # row vector
np.dot(a,a.T)
->[[ 0.72596923 -0.62681262  1.45607162  0.9602874   0.78054954]
   [-0.62681262  0.54119932 -1.25719386 -0.8291264  -0.67393806]
   [ 1.45607162 -1.25719386  2.92043309  1.926042    1.56554298]
   [ 0.9602874  -0.8291264   1.926042    1.2702355   1.03248437]
   [ 0.78054954 -0.67393806  1.56554298  1.03248437  0.83923334]]
```

→ 위와 같이 array를 만들 경우 (5,1) : column vector , (1,5) : row vector 로 생성이 됨. 이는 코드 연산 시 simple하게 사용가능 하므로 반드시 위와 같은 형태로 사용해야 함!!

즉, **Don't use rank 1 array, Use (n\*1) or (1\*n) matrix !!**

