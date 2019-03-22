---
layout: post
title: "[A Multimodal Anomaly Detector for Robot-Assisted Feeding Using an LSTM-based Variational Autoencoder] Paper Review"
author: "박상민"
date: 2019-03-22 18:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection, LSTM-VAE]
---

본 포스트는 로봇 시스템에 딥러닝 LSTM-VAE모델을 적용한 논문을 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.
> 
> 아직 지식이 많이 부족하고, 경험이 부족하기 때문에, 고칠 것도 많을 것 같습니다. 고처야 할 부분은 언제든지 연락주시면 감사하겠습니다 :)

#  개요

이번글은 간략하게 읽은 여러 논문 중 세 번째 논문에 대해 정리한 글 입니다. 

논문을 조사하고 읽은 목적은 다른 곳에서는 어떤식으로 데이터를 구축하는지, 어떤 문제를 해결하려고 하였는지, 모델 성능평가는 어떻게 하는지, 어떤 방법으로 연구하는지 등의 인사이트를 얻기 위해 간단하게 조사한 것 입니다. 논문 중 꼭 자세히 읽어야 하는  부분은 좀 더 자세히 읽고, 개별 포스트를 만들어 정리하였습니다.
    
아래는 제가 읽은 논문들 중 10개에 대해서 간단하게 분류한 것 입니다.  
![Paper]({{ "/images/2019/paper_1.png" | prepend: site.baseurl }})

위 사진을 보면 어떤 논문이 어떤 모델을 썼는지, 시계열 데이터 사용 유무 등을 한번에 볼 수 있습니다. 예를들어 5번 논문의 경우 시게열 데이터를 사용했고, SVM 모델을 사용했습니다. 원이 겹쳐져있는 경우는 두 개를 같이 사용했다는 뜻 입니다. 즉, 5번 논문은 SVM모델과 DNN + LSTM를 동시에 사용한 모델이라는 뜻 입니다.

번역을 잘못하거나, 잘못 이해한 부분이 있다면 언제든지 말씀해주시면 반영하도록 하겠습니다!!


# 3. A Multimodal Anomaly Detector for Robot-Assisted Feeding Using an LSTM-based Variational Autoencoder [3](https://arxiv.org/pdf/1711.00614.pdf)

* 본 논문의 동기는 밥을 먹는데 도와주는 로봇이 구조적, 하드웨어적 문제로 종종 오류가 발생해서 발생한 오류(이상)들을 감지하는 시스템을 개발하는 것이었습니다.

* 구조적, 하드웨어적 이상들을 감지하는 시스템이 없다면 로봇이 자주 고장나게 되고, 수리비용이 높아지며, 사용자들이 더 이상 사용하지 않을 수 있는 문제점이 있다고 합니다.

* 비정상적인 이상 상황들을 검출하고, 인식한다면 미리 예방이 가능하다고 논문에서는 말하고 있습니다.

* LSTM-VAE(LSTM based variational autoencoder)를 이용해 Anomaly Score를 계산하였습니다. 

    ![Paper_3]({{ "/images/2019/paper_3.png" | prepend: site.baseurl }})

* Anomaly Score가 Threshold를 넘어서게 되면 이상이라고 판단을 합니다.

* 논문에서는 기존의 여러 방법들을 적용해 보았지만 LSTM-VAE모델의 성능이 가장 좋았다고 합니다.
