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
> 
> 아직 지식이 많이 부족하고, 경험이 부족하기 때문에, 고칠 것도 많을 것 같습니다. 고처야 할 부분은 언제든지 연락주시면 감사하겠습니다 :)

#  개요

이번글은 간략하게 읽은 여러 논문 중 일곱 번째 논문에 대해 정리한 글 입니다. 

논문을 조사하고 읽은 목적은 다른 곳에서는 어떤식으로 데이터를 구축하는지, 어떤 문제를 해결하려고 하였는지, 모델 성능평가는 어떻게 하는지, 어떤 방법으로 연구하는지 등의 인사이트를 얻기 위해 간단하게 조사한 것 입니다. 논문 중 꼭 자세히 읽어야 하는  부분은 좀 더 자세히 읽고, 개별 포스트를 만들어 정리하였습니다.
    
아래는 제가 읽은 논문들 중 10개에 대해서 간단하게 분류한 것 입니다.  
![Paper]({{ "/images/2019/paper_1.png" | prepend: site.baseurl }})

위 사진을 보면 어떤 논문이 어떤 모델을 썼는지, 시계열 데이터 사용 유무 등을 한번에 볼 수 있습니다. 예를들어 5번 논문의 경우 시게열 데이터를 사용했고, SVM 모델을 사용했습니다. 원이 겹쳐져있는 경우는 두 개를 같이 사용했다는 뜻 입니다. 즉, 5번 논문은 SVM모델과 DNN + LSTM를 동시에 사용한 모델이라는 뜻 입니다.

번역을 잘못하거나, 잘못 이해한 부분이 있다면 언제든지 말씀해주시면 반영하도록 하겠습니다!!


# 7. Anomaly Detection with Generative Adversarial Networks for Multivariate Time Series [7](https://arxiv.org/pdf/1709.05342.pdf)

* 오늘날 CPS 시스템은 크고, 복잡하며, 사이버 공격의 목표가 되는 network sensor와 actuators가 부착되어 있다고 눈문에서는 설명합니다.

* 기존의 이상감지 기법 들은 역동적이고, 복잡한 것 들을 감지할 수 없다는 단점을 논문에서는 밝힙니다.

* 비지도학습(Unsupervised)기반의 머신러닝 기법을 이용해 비정상적인 동작을 공격으로 분류할 수 있다고 합니다.

* 본 논문에서는 복잡한 네트워크를 위한 새로운 Generative Adversarial Networks-based Anomaly Detection(GAN-AD) 방안을 제안하였습니다.

* GAN모델 내에있는 LSTM-RNN이 다변수 시계열 데이터의 분포를 capture합니다.

* 각 센서와 액추에이터 시계열 데이터를 독립적으로 처리하는 대신, 시계열 데이터를 동시에 모델링하여 잠재적인 상호작용을 고려한다고 설명합니다.

* Secure Water Treatment Testbed(SWaT) 데이터 셋을 사용해 테스트를 하였으며, 다른 비지도학습 이상감지 기법보다 성능이 좋았다고 말하고 있습니다.

    ![Paper_7]({{ "/images/2019/paper_7.png" | prepend: site.baseurl }})