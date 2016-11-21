---
published: true
title: Neural Networks and Deep Learning
layout: post
author: Kwangjin Yoon 
category: Deep learning, Neural Network, Backpropagation
tags: 
- Deep learning 
- Neural Network
- backpropagation
- 역전파
- 번역
---

<q>이 글은 Michael Nielsen의 책 [Neural Networks and Deel Learning](http://neuralnetworksanddeeplearning.com/chap1.html)를 번역한 것 입니다. **현재 번역 중 입니다.**</q>

## Chapter 2: 역전파<sup>backpropagation</sup> 알고리즘의 원리

* Table of Contents
{:toc}

지난 챕터에서는 신경망이 gradient descent 알고리즘을 이용해 어떻게 weight와 bias들을 학습해 가는지 알아 보았다. 그런데 우리는 Cost function의 gradient를 어떻게 계산하는 지는 알아보지 않았다. 이번 챕터에서는 역전파<sup>backpropagation</sup>라고 불리우는 Cost function의 gradient를 빠르게 계산하는 알고리즘을 공부해보자.  

<!-- more -->

Backpropagation은 1970년대에 처음 소개되었지만, 1986년 [David Rumelhart](http://en.wikipedia.org/wiki/David_Rumelhart), [Geoffery Hintton](http://www.cs.toronto.edu/~hinton/), [Ronald Williams](http://en.wikipedia.org/wiki/Ronald_J._Williams)의 유명한 [논문](http://www.nature.com/nature/journal/v323/n6088/pdf/323533a0.pdf)에의해서 그 중요성이 알려지게 되었다.  

*작성 중* 