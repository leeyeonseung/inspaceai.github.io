---
layout: post
title: "[Anomaly Detection with Generative Adversarial Networks for Multivariate Time Series] Paper Review"
author: "박상민"
date: 2019-03-22 15:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection, GAN]
---

본 포스트는 CPS 시스템에 GAN을 이용해 이상감지 모델을 적용한 논문에 대해 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.

# 7. Anomaly Detection with Generative Adversarial Networks for Multivariate Time Series [7](https://arxiv.org/pdf/1709.05342.pdf)

* 오늘날 CPS 시스템은 크고, 복잡하며, 사이버 공격의 목표가 되는 network sensor와 actuators가 부착되어 있다고 눈문에서는 설명합니다.

* 기존의 이상감지 기법 들은 역동적이고, 복잡한 것 들을 감지할 수 없다는 단점을 논문에서는 밝힙니다.

* 비지도학습(Unsupervised)기반의 머신러닝 기법을 이용해 비정상적인 동작을 공격으로 분류할 수 있다고 합니다.

* 본 논문에서는 복잡한 네트워크를 위한 새로운 Generative Adversarial Networks-based Anomaly Detection(GAN-AD) 방안을 제안하였습니다.

* GAN모델 내에있는 LSTM-RNN이 다변수 시계열 데이터의 분포를 capture합니다.

* 각 센서와 액추에이터 시계열 데이터를 독립적으로 처리하는 대신, 시계열 데이터를 동시에 모델링하여 잠재적인 상호작용을 고려한다고 설명합니다.

* Secure Water Treatment Testbed(SWaT) 데이터 셋을 사용해 테스트를 하였으며, 다른 비지도학습 이상감지 기법보다 성능이 좋았다고 말하고 있습니다.

    ![Paper_7]({{ "/images/sangmin/paper_7.png" | prepend: site.baseurl }})