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

![image-20210202001338622](\assets\img\2021-02-02\figure1.jpg){: .align-center}

### 1) 용어정리

$$N$$ : audio(voice) recording의 수

$$M$$ : speaker의 수

$$u$$ : 특정 speaker를 나타내는 speaker id

$$N_u$$ : speaker $$u$$가 가진 voice samples의 수

$$\mathcal{L}$$