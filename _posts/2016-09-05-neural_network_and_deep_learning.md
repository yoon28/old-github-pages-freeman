---
published: true
title: Neural Networks and Deep Learning-Chapter1
layout: post
author: Kwangjin Yoon 
category: 
- Deep learning
- Neural Network
tags: 
- Deep learning 
- Neural Network
- 번역
---

<q>이 글은 Michael Nielsen의 책 [Neural Networks and Deel Learning](http://neuralnetworksanddeeplearning.com/chap1.html)를 번역한 것 입니다. **현재 번역 중 입니다.**</q>


## Chapter 1: Neural net을 이용한 손글씨 숫자<sup>Handwritten digits</sup> 인식

* Table of Contents
{:toc}


사람의 시각 시스템은 세상에서 우리가 이해하지 못하는 것들 중에 하나다. 다음 사진 속의 손으로 쓴 일련의 숫자들을 보아 보자.

![imgs 1](http://neuralnetworksanddeeplearning.com/images/digits.png){:width="30%" }
{: .center}

<!-- more -->

사람들은 어렵지 않게 위의 숫자들이 504192 임을 인식한다. 우리의 뇌에는 V1이라 불리는 시각 피질이 있고 이곳에는 뉴런들이 약 1억 4천개 정도 있으며 이들 간의 연결은 수백억에 달 한다.
하지만 사람의 시각 시스템이 V1만으로 이루어진 것은 아니고, 좀더 복잡한 영상 처리 작업을 하는 V2, V3, V4, V5 라 불리는 일련의 시각 피질이 존재한다.
우리가 사람의 머리를 슈퍼컴퓨터로 옮기고 수 백만년의 진화(업데이트)를 통해 가시 세계를 이해 할 수 있도록 해보자. 손글씨 숫자<sup>Handwritten digits</sup>를 인식하게 하는 것은 여전히 어려울 것이다. 하지만 인간들은 아주 훌률하게도 눈으로 보는 것을 아주 쉽게 이해하며, 심지어는 무의식 중에도 그러한 일을 처리한다. 그래서 인간들은 그러한 우수한 시각 능력에 그다지 감사함을 느끼진 않는다.

그런데 우리가 손글씨 숫자 인식이 가능한 컴퓨터 프로그램을 만들어보려고 하면 비로소 그러한 시각 인지 능력<sup>Visual Pattern Recognition</sup>이 어려운 일이라는 것을 깨닫게 된다.
우리가 직접 할때는 굉장히 쉬웠던 것이 굉장히 어려워지는 순간이다. 우리가 숫자 "9"를 인식할때를 생각해보자-"윗 부분에 동그라미가 있고 아랫부분에는 수직선이 있다"-라는 직관을 알고리즘으로 기술 하는 것은 쉬운일이 아니다.
그러한 알고리즘을 만드려는 시도는 무한한 예외처리 및 특정 케이스 핸들링에 시달리게 된다. 절망에 빠지는 순간이다.

![imgs 2](http://neuralnetworksanddeeplearning.com/images/mnist_100_digits.png){:width="50%"}
{: .center}

뉴럴 네트워크<sup>Neural Network</sup>는 이와 같은 문제를 다른 방법으로 다룬다.
핵심은 트레이닝 데이터라고 불리우는 수 많은 손글씨 숫자를 이용해 학습을 하는 시스템의 개발이다.
즉, 뉴럴 네트워크는 트레이닝 데이터를 통해 손글씨 숫자를 인식할 수 있는 규칙을 스스로 학습한다.
또한, 트레이닝 데이터의 수를 늘림으로써 뉴럴 네트워크는 더 많이 배우게 되며 그 정확도 역시 상승한다. 위의 사진에는 100개의 손글씨 숫자들이 있는데, 수천 또는 수백만, 수십억개의 트레이닝 데이터를 이용한다면 더 나은 손글씨 숫자 인식기를 만들 수 있을 것이다.

이 챕터를 통해 손글씨 숫자를 인식 할 수 있는 뉴럴 네트워크 프로그램을 만들어 볼 것이다. 프로그램은 74줄 정도에 불과하고 뉴럴 네트워크에 관련된 특별한 라이브러리를 사용하지도 않는다.
그럼에도 이 프로그램은 손글씨 숫자 인식률이 96%에 달한다. 첨언하자면, 상용 뉴럴 네트워크 프로그램 중에는 은행이나 우체국에 적용되어 수표를 검수하거나 주소를 인식하는데 사용되기도 한다.

여기서는 손글씨 숫자를 인식하는데 중점을 두기로 한다. 왜냐하면 여러분들이 뉴럴 네트워크를 학습하는데 매우 훌률한 예제이기 때문이다.
즉, 예제로써 손글씨 숫자 인식은 높은 인식률을 달성하기에는 어렵지만, 해결책 자체는 많이 어렵지 않은 장점을 가지고 있다.   
또한, 딥러닝<sup>Deep Learning</sup>과 같은 진보된 기술 개발에도 사용할 것이다. 이 책 전반을 통해 손글씨 숫자 인식 예제를 사용할 것이다.
그리고 책 후반에는 뉴럴 네트워크를 컴퓨터 비젼<sup>Computer Vision</sup>이나 음성 인식, NLP<sup>Natural Language Processing</sup> 등 다른 분야에 적용하는 방법에 대해서도 이야기 하겠다.  

물론 정말 손글씨 숫자를 인식하는 프로그램만 개발하는 것이 이 챕터의 목적이었다면 이 챕터는 당연히 더 짧았을 것이다! 하지만 여기서는 뉴럴 네트워크 개발에 필요한 중요한 컨셉들과 함께 두 개의 중요한 인공 뉴런<sup>Artificial neuron</sup>(퍼셉트론<sup>Perceptron</sup>과 시그모이드 뉴런<sup>Sigmoid neuron</sup>) 그리고 통계적 그라디언트 디센트<sup>Stochastic Gradient Descent</sup>라 불리는 학습 알고리즘<sup>Learning Algorithm</sup>을 다룰 것이다.  
전반적으로, 나는 독자가 뉴럴 네트워크의 동작 원리에 대한 직관을 형성할 수 있도록 자세히 설명할 것이다. 단순히 메카니즘을 설명하는 방식보다는 설명이 길어지겠지만 학습자가 공부하는 데에는 더 나은 방법일 것이다.
그렇게 이 챕터를 다 읽고나면 딥러닝이 무엇인지, 왜 그것에 주목하는지에 대해 이해하게 될 것이다.   
<br> 

### Perceptrons

뉴럴 네트워크란 무엇일까? 시작하기에 앞서 인공 뉴런 중 하나인 퍼셉트론 부터 짚고 넘어가자.
퍼셉트론은 1950, 60년대에 걸쳐 [Frank Rosenblatt](http://en.wikipedia.org/wiki/Frank_Rosenblatt)에 의해 [개발](http://books.google.ca/books/about/Principles_of_neurodynamics.html?id=7FhRAAAAMAAJ)되었으며 [Warren McCulloch](http://en.wikipedia.org/wiki/Warren_McCulloch)와 [Walter Pitts](http://en.wikipedia.org/wiki/Walter_Pitts)의 선행 [연구](http://scholar.google.ca/scholar?cluster=4035975255085082870)로부터 영향을 받았다.
오늘날에는 *시그모이드 뉴런<sup>sigmoid neuron</sup>*이라 불리는 인공뉴런이 더욱 자주 사용되어지고 있으며 이 책에서도 주로 언급된다. 곧 시그모이드 뉴런에 대해 살펴볼 예정이지만 우선 퍼셉트론의 원리부터 이해함으로써 시그모이드 뉴런을 쉽게 이해할 수 있도록 할 것이다.

그러면 퍼셉트론은 어떻게 동작할까? 퍼셉트론은 여러개의 바이너리<sup>binary</sup> 변수, $$ x_{1}, x_{2}, ... , $$ 를 입력으로 받아 하나의 바이너리 출력을 발생 시킨다:

 
![imgs 3](http://neuralnetworksanddeeplearning.com/images/tikz0.png){:width="50%"}
{: .center}

위 그림의 퍼셉트론은 세 개의 입력 $$ x_{1}, x_{2}, x_{3} $$ 을 이용한다. Rosenblatt은 이것의 결과를 계산할 수 있는 간단한 방법을 제안하였다. 각 입력의 중요도를 나타내는 실수 가중치 $$ w_{1}, w_{2}, ... $$ 을 이용한 방법이다. 
뉴런은 계산 결과로 0 또는 1의 값을 갖는데 가중치와 입력의 곱들의 합, 즉 $$ \sum_{j}w_{j}x_{j} $$ 이 특정 임계값<sup>threshold</sup>을 넘는지 안 넘는지에 의해 결정 지어 진다.



*작성 중*


