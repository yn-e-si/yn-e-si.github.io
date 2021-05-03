---
title: "[Programmers Dev] 표본 분포 (Sampling Distribution)"
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

## &#128161; 표본 분포 (Sampling Distribution)

### &#128204; 표본 조사의 필요성과 표본 추출 방법

통계적 추론

- 전수 조사는 실질적으로 불가능한 경우가 많다.

> &#128173; 시간과 비용이 많이 소요되기 때문

- 그래서 보통 표본 조사를 통해 모집단에 대한 해석을 진행한다.

> &#128173; 하지만 표본 조사는 반드시 오차가 발생하게 된다. 따라서 적절한 표본 추출 방법이 필요하고 표본과 모집단과의 관계를 잘 이해해야 오차를 줄일 수 있다.

<br/>

표본 추출 방법

- 단순랜덤추출법 (random sampling)
- 난수표 사용
- 랜덤 넘버 생성기 사용

```python
import random
[random.randint(1, 10) for i in range(10)]
```

> &#128173; 이 외에도 여러가지 방법이 존재한다.

<br/>

### &#128204; 표본 분포

모수와 통계량

- 표본조사를 통해 파악하고자 하는 정보
  - 모수 (Parameter)
    - 모집단의 특성치
    - 관심의 대상이 되는 모집단의 대표값
- 모수의 종류
  - 모평균, 모분산, 모비율 등이 있다.
  - 모수를 추정하기 위해 표본을 선택하여 표본 평균이나 표본 분산 등을 계산하게 된다.

- 통계량 (statistic)
  - 표본 평균이나 표본 분산과 같은 표본의 특성값

<br/>

예) 표본분포

50 만명의 전국 고등학교 1 학년 학생의 키를 조사하기 위해 1000 명을 표본을 조사했을 때, 표본의 평균을 계산한다고 가정해보자.

- 이 때, 표본의 평균은 표본의 선택에 따라 값이 달라지게 된다.

> &#128173; 1000 명이라는 제한된 표본은 매번 1000 명을 새로 뽑을 때마다 그 특성이 달라지기 때문

- 따라서 표본평균은 확률변수이고, 확률변수이기에 표본평균이 가질 수 있는 값도 하나의 확률분포를 가지게 된다.

> &#128173; 이 분포가 무엇인지가 표본을 해석하는데 있어 매우 중요한 역할을 하게 된다.

<br/>

&#128073; 이러한 통계량의 확률분포를 표본분포 (Sampling distribution) 라고 한다.



여러가지 모수 중에 보통 가장 관심을 가지고 있는 모수는 모평균이다.

따라서 이번 강의에서는 여러 모수 중 모평균에 대해 설명하고 있다.

- 표본평균

  - 모평균을 알아내는데 쓰이는 통계량

- 표본평균의 분포

  - $x_1, x_2, \cdots, x_n$
    - 평균: $ \mu $ , 분산: $\sigma ^2 $
    - **정규모집단에서** 추출된 표본의 측정값

  - 표본평균
    - $ \bar{x} = \frac{1}{n}\sum^n_{i=1}x_i $
    - $\bar X \sim N \left (\mu,\frac{\sigma^2}{n}\right)$

> &#128173; 표본평균에서는 $n$ 이 크면 클수록 분산이 작아지고, 분산이 작아지면 $ \bar x $ 값이 모평균에 가까워지게 된다. 즉, $ㅜ$ $n$ 이 클수록 표본평균은 모평균에 가까워지게 된다.

<br/>

예1)  모집단이 정규분포를 따른다는 것을 가정.

```python
import numpy as np
import matplotlib.pyplot as plt

xbars = [np.mean(np.random.normal(size=10)) for i in range(10000)]
print("mean%f, var%f" %(np.mean(xbars), np.var(xbars)))
h = plt.hist(xbars, range = (-2, 2), bins = 30)
```

![](https://yn-e-si.com/assets/images/program_dev/sampling_distribution_1.JPG){: .align-center}

<br/>

예2) 모집단이 정규분포를 따른다는 것을 가정.

```python
import numpy as np
import matplotlib.pyplot as plt

# loc: mean, scale: standard deviation
xbars = [np.mean(np.random.normal(loc=10, scale=3, size = 10)) for i in range(10000)]
print("mean %f, var %f"%(np.mean(xbars), np.var(xbars)))
h = plt.hist(xbars, range = (5, 15), bins = 30)
```

![](https://yn-e-si.com/assets/images/program_dev/sampling_distribution_2.JPG){: .align-center}

<br/>

위의 예시는 모집단이 정규분포를 따른다고 가정하여서 표본평균을 구할 수 있었다.

만약, 모집단이 정규분포가 아닌 어떤 다른 분포를 따른다고 했을 때, 표본평균은 어떻게 구할 수 있을까?

<br/>

위의 질문에 대한 답으로 <code>중심극한정리</code>가 있다.



### &#128204; 중심극한정리 (Central Limit Theorem)

- $x_1, x_2, \cdots, x_n$
- 평균: $ \mu $, 분산: $\sigma^2$
- 위에 평균과 분산은 모집단에서 추출된 표본의 측정값이다.

> &#128173; 단, 모집단은 정규분포가 아니고 어떤 분포를 따르는 지는 모른다고 가정한다.

<br/>

이 때, 표본평균은 평소와 같이 다음처럼 구할 수 있다. 하지만 모집단이 정규분포를 따르지 않기 때문에 표본평균이 정규분포를 따른다고 할 수 없다.

- $\bar x = \frac{1}{n} \sum^n_{i=1} x_i$

하지만  $n$ 이 충분히 큰 경우 $ (n \geq 30)$,

- **근사적으로** $ \bar X \sim N \left(\mu, \frac{\sigma^2}{n}\right)$ 를 따른다.

> &#128173; 모집단이 정규분포가 아닌 어떤 분포를 따르는지 모를경우, 30 개 이상의 표본을 선택할 경우에만 표본평균은 근사적으로 정규분포를 따른다는 것이 중심극한정리의 개념이다.

<br/>

예)

모집단의 정보

- Uniform Distribution
- $E(X) = 5, Var(X) = \frac {(10-0)^2}{12} = 8.3$

<br/>



- $n=3$

```python
import numpy as np
import matplotlib.pyplot as plt
n = 3
xbars = [np.mean(np.random.rand(n)*10) for i in range(10000)]
print("mean %f, var %f" %(np.mean(xbars), np.var(xbars)))
h = plot.hist(xbars, range=(0,10), bins = 100)
```

![](https://yn-e-si.com/assets/images/program_dev/sampling_distribution_3.JPG){: .align-center}

- n = 5

![](https://yn-e-si.com/assets/images/program_dev/sampling_distribution_4.JPG){: .align-center}

- n = 10

![](https://yn-e-si.com/assets/images/program_dev/sampling_distribution_5.JPG){: .align-center}

- n = 30

![](https://yn-e-si.com/assets/images/program_dev/sampling_distribution_6.JPG){: .align-center}

&#128073; $n$ 이 커지면 커질수록, 정규분포에 가까워짐을 알 수 있다.





<br/>

<br/>

## &#128161; Check Point

- 표본평균은 표본을 어떻게 뽑느냐에 따라서 값이 달라질 수 있기에 **확률변수**이다.
- 또한 확률변수이기에 **확률분포**를 갖게 된다.
- 정규분포일 경우 $n$ 의 크기에 상관없이 표본평균의 분포는 정규분포를 따르고, 모집단의 분포가  정규분포가 아닌 다른 분포일 경우 $n$ 이 $ (n \geq 30)$ 커지면 커질수록 정규분포를 따르게 된다. 이를 **중심극한정리**라 한다.