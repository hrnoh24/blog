---
layout: single
title: "[ICLR 2021] Improving Zero-Shot Voice Style Transfer via Disentangled Representation Learning 요약"
author: 초코
excerpt: Improving Zero-Shot Voice Style Transfer via Disentangled Representation Learning 논문을 요약해보았습니다.

date: 2021-02-02
last_modified_at: 2021-02-02

categories:
  - papers
tags:
  - Voice Conversion
toc: true
toc_sticky: true
use_math: true
comments: true
---







# Goal

Zero-shot voice conversion을 수행하는 것<br>

<br>

# Limitations in existing methods

1. AutoVC [[paper](https://arxiv.org/abs/1905.05879)]의 문제점
   * Content encoder가 style 정보를 encoding 하지않음을 보장해주는 regularizer가 없다.
2. AdaIN-VC [[paper](https://arxiv.org/abs/1904.05742)]의 문제점
   * Style embeddings에서 content 정보를 지우지 못했다.

<br>

# Contribution

1. Information-theoretic Disentangled Embedding for Voice Conversion (IDE-VC)을 제안했다.
   * Content embeddings과 style embeddings의 mutual information을 최소화하여 두 정보 사이의 disentanglement를 효과적으로 달성했다.
   * Latent embeddings의 representativeness를 향상시키기 위해 2개의 새로운 multi-group mutual information lower bounds를 유도했다.

<br>

# Method

![Training and transfer process]({{'assets/img/2021-02-02/figure1.jpg' | relative_url}}){:.img-responsive.align-center}

*Training and transfer 과정. 왼쪽: style encoder $$E_s$$를 $$\hat{\mathcal{I}}_1$$를 통해 훈련하는 과정. 가운데: $$\hat{\mathcal{I}}_2, \hat{\mathcal{I}}_3$$을 통해 Content encoder $$E_c$$와 Decoder를 훈련하는 과정. 오른쪽: Speaker $$u$$의 음성인 $$x_{ui}$$로부터 content information을 추출하고 Speaker $$v$$의 음성인 $$x_{vi}$$로부터 style information을 추출하여 이를 Decoder에 넣어 voice style transfer를 수행하는 과정*

### 1) 용어정리

$$N$$ : audio(voice) recording의 수

$$M$$ : speaker의 수

$$u$$ : 특정 speaker를 나타내는 speaker id

$$N_u$$ : speaker $$u$$가 가진 voice samples의 수



### 0. Background

* MI (Mutual information)이란? [참조](https://blueskyvision.tistory.com/m/774?category=786439)

  * 수학적 정의

    $$I(X;Y):=\sum_{x,y}p(x,y)\log\frac{p(x,y)}{p(x)p(y)}$$
    * $$p(x,y)$$ : joint distribution
    * $$p(x)$$ : $$x$$의 marginal distribution
    * $$p(y)$$ : $$y$$의 marginal distribution

  * 개념

    * 하나의 확률변수가 다른 하나의 확률변수에 대해 제공하는 정보의 양

* MI maximization tasks를 위한 MI estimator

  * Nguyen, Wainwright, and Jordan (NWJ)의 estimator [[paper](https://arxiv.org/abs/0809.0853)]

    $$\mathcal{I}_{NWJ}:=\mathbb{E}_{p(x,y)}[f(x,y)]-e^{-1}\mathbb{E}_{p(x)p(y)}[e^{f(x,y)}]$$