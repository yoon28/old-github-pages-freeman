---
published: true
title: Minimum cost flow
layout: post
author: Yu 
category: news
tags:
- version
---

## Minimum cost flow problem
Minimum cost flow(MCF) 문제는 주어진 그래프와 제약 조건을 만족하는 최소 비용의 flow를 구하는 문제이다.

<br>

### MCF의 그래프 
MCF에서 그래프는 노드(Node)와 방향성이 있는 간선(Edge)으로 이루어져있다. 즉, 그래프 $$G=(V,E)$$의 모든 간선 $$(i,j)\in E$$는 노드 $$i$$에서 노드$$j$$로 흐르는 방향의 간선이다. 이때 $$i,j \in V$$이다. 또 모든 간선들은 **capacity** $$u_{ij}$$와 **cost** $$c_{ij}$$를 갖는다. $$u_{ij}$$는 간선 $$(i,j)$$에 흐를수 있는 **최대 flow**를 나타내며, $$c_{ij}$$는 간선 $$(i,j)$$를 흐르는 **하나의 flow당 소요되는 cost**를 말한다. 그리고 모든 노드 $$i \in V$$는 **supply** $$b_{i}$$를 갖는다. $$b_{i}$$가 $$0$$보다 클 경우 노드 $$i$$를 **supply node**라 부르고, $$b_{i}<0$$이면 **demand node**라 부른다. 만약 $$b_{i}=0$$이면 **transshipment node**라 부른다. 아래 사진은 MCF 그래프의 한 예이다. 6개의 노드와 7개의 간선으로 이루어진 것을 확인 할 수 있다. 예제로부터 간선 $$(1,3)$$은 3의 **capacity**와 4의 **cost**를 가지며 노드 1은 $$b_{1}$$ 값이 5이므로 **supply node**이다. 

{: .center}
![graph example](http://community.topcoder.com/i/education/minimumCostFlow/Figure_1_1.png "graph example")

{:.center}
<sub>*위 그림은 [topcoder](https://www.topcoder.com/community/data-science/data-science-tutorials/minimum-cost-flow-part-one-key-concepts/) 에서 발췌한 것 입니다.*</sub>

<br>

### MCF의 제약 조건
간선 $$(i,j)\in E$$를 흐르는 flow를 $$x_{ij}$$라고 하자. 그러면 MCF 문제는 다음의 값을 최소화하는 최적화 문제이다.

$$ \min_{x_{ij}} \sum_{(i,j)\in E} c_{ij}x_{ij} $$  

더불어 다음의 두가지 제약 조건을 만족하여야 한다.

$$ \sum_{(i,j)\in E}x_{ij} - \sum_{(j,i)\in E}x_{ji} = b_{i} \text{, for all } i \in V $$

$$ 0 \leq x_{ij} \leq u_{ij} \text{, for all } (i,j)\in E $$

첫 번째 제약 조건을 **flow conservation constraint**라고 부른다. 이 제약 조건은 어떤 노드 $$i$$에서 **나가는 flow의 총합**과 **들어오는 flow의 총합**의 차이가 $$b_{i}$$와 같아야 함을 말한다. 두 번째 제약 조건은 간선 $$(i,j)$$를 흐르는 flow $$x_{ij}$$의 크기에 대한 제약 조건인데 이 크기가 0보다 크거나 같고 **capacity** $$u_{ij}$$보다 작거나 같아야함을 말한다.

*작성 중..*
