---
title: "[Google Bootcamp] 1. Neural Networks and Deep Learning"
excerpt: "Week1: Introduction"
categories:
 - DL
tags:
 - Google Bootcamp
 - Coursera
 - Deep Learning
---

이 포스팅은 *[Google Machine Learning Bootcamp]* 중 *[Coursera - Deep Learning Specialization Course by Andrew Ng]*의 *review*를 위해 작성된 포스팅 입니다.

![](C:\Users\leejy\yn-e-si.github.io\assets\images\image-1.png){: .align-center}

**neuron이 하는 역할**은 size(x)를 input value로 받고,  price(y)를 output으로 출력할 수 있는 **일차함수**를 만드는 것이다.

![](C:\Users\leejy\yn-e-si.github.io\assets\images\image-2.png){: .align-center}

위의 함수와 같이 최대값을 0으로 갖고 점점 증가하는 1차함수를 Relu(Rectified linear units)라 한다.

![](C:\Users\leejy\yn-e-si.github.io\assets\images\image-3.png){: .align-center}

이렇게 하나의 neuron으로 이루어져 있는 것을 **single neural network** 라고 한다.

따라서 neuron들이 점차 쌓여가면 더 큰 neural network가 만들어 진다.

![](C:\Users\leejy\yn-e-si.github.io\assets\images\image-4.png){: .align-center}

4가지의 input들을 X, 예측하려는 price를 Y, 그리고 여기서 보이는 작은 동그라미들이 각각 Relu 함수라고 보면 된다.

위에서 처음 봤던 single neural network와는 다르게 neuron들과 layer를 쌓아가면서 좀 더 큰 neural network가 만들어 짐을 볼 수 있다.

→ 즉, **neuron**과 **layer**들을 쌓아가면서 **neural network**의 크기를 조절해줄 수 있다.

neural network의 특징은 이를 학습시킬 때 input으로 x를, output으로 y를 training set에 주면 된다.

가운데 부분은 알아서 해결되는 데, 이 때 보통 정해주는 것은 **neuron의 수**, **layer의 수** 그리고 **function의 종류** 정도라 생각하면 된다.

![](C:\Users\leejy\yn-e-si.github.io\assets\images\image-5.png){: .align-center}

이 예제에서 보자면, 현재 4개의 input을 갖고 최종적으로 price(y)를 예측해 내는 neural network라고 볼 수 있다.

이 neural network를 좀 더 분해 해보면,

가장 좌측에 x로만 이루어져 있는 부분을 **input layer**, 가장 우측에 최종 예측값을 나타내는 부분을 **output layer**라고 한다. 이를 제외한 가운데에 있는 부분을 가려져 있다해서 **hidden layer**라고 한다.

즉, 여기서는 2개의 hidden layer를 가지고 있다. 그리고 각 hidden layer에 있는 동그라미 부분을 **hidden unit**이라고도 하는데 이는 위에서 언급했던 Relu와 같이 function들이 적용되는 부분이라고 생각하면 된다.

![](C:\Users\leejy\yn-e-si.github.io\assets\images\image-6.png){: .align-center}

*Supervised Learning*

- target label이 존재한다.
- **input - output** 간의 **pair**로 이루어져 있다.

![](C:\Users\leejy\yn-e-si.github.io\assets\images\image-7.png){: .align-center}

*Standard NN* - 일반적인 NN

*Convolutional NN* - **이미지** 데이터에 주로 사용

*Recurrent NN* - **시간적인 요소**를 담고 있는 일차원적인 데이터를 다루는데 주로 사용

![](C:\Users\leejy\yn-e-si.github.io\assets\images\image-8.png){: .align-center}

*Structured Data(정형 데이터)*

- Database들의 data라고 볼 수 있다.
- feature들의 값이 명확한 뜻을 정의하고 있어야한다.

→ **즉, Structured Data는 Database형태로 저장되어 있는 data들이라 할 수 있지만 각 값들은 명확한 뜻을 가지고 있는 값들이어야 한다.**

*Unstructured Data(비정형 데이터)*

- Structured Data와 반대되는 데이터이다.
- 이미지, 텍스트, 오디오과 같은 내용을 인식하고자 하는 데이터이다.
- feature들의 값이 명확한 뜻을 정의하고 있지 않다.

→ **즉, Unstructured Data는 Structured Data와 달리 규칙적으로 저장되어 있는 data가 아니며 각 값들은 명확한 뜻을 가지고 있지 않다.**

![](C:\Users\leejy\yn-e-si.github.io\assets\images\image-9.png){: .align-center}

High performance를 위한 2가지

- large neural network를 가질 수 있어야 한다.
- 많은 양의 데이터가 필요 → size of neural network, hidden units, large amount of variables and scale of data etc.

**small training sets**일 경우, 보통 **engineering skills**에 따라 performance가 정해질 수 있다.

오직 **large training sets**일 때, **large NN**이 performance가 더 높다라고 할 수 있다.

![](C:\Users\leejy\yn-e-si.github.io\assets\images\image-10.png){: .align-center}

large data를 fast computation하려는 시도 

​					→ deep learning algorithms이 큰 발전을 하는데 기여

fast computation이 중요한 이유

- neural network를 training하는 과정이 반복적이다.
- Idea - Code - Experiment 라는 반복적인 과정 -> fast computation일 수록 experiment의 결과를 확인하는데 큰 도움을 준다.
- 이는 반복업무를 더 빠르게 하는 것이 가능케하고 idea를 빠르게 개선시킬 수 있게 해준다.

→ 따라서 **Fast computation**일 수록, **Algorithms**의 **feedback**이 빠르게 되어 발전에 큰 영향을 줄 수 있다.



##### Reference

[source]  <https://www.coursera.org/learn/neural-networks-deep-learning>