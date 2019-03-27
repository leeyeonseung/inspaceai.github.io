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


# 3. A Multimodal Anomaly Detector for Robot-Assisted Feeding Using an LSTM-based Variational Autoencoder [3](https://arxiv.org/pdf/1711.00614.pdf)

* 본 논문의 동기는 밥을 먹는데 도와주는 로봇이 구조적, 하드웨어적 문제로 종종 오류가 발생해서 발생한 오류(이상)들을 감지하는 시스템을 개발하는 것이었습니다.

* 구조적, 하드웨어적 이상들을 감지하는 시스템이 없다면 로봇이 자주 고장나게 되고, 수리비용이 높아지며, 사용자들이 더 이상 사용하지 않을 수 있는 문제점이 있다고 합니다.

* 비정상적인 이상 상황들을 검출하고, 인식한다면 미리 예방이 가능하다고 논문에서는 말하고 있습니다.

* LSTM-VAE(LSTM based variational autoencoder)를 이용해 Anomaly Score를 계산하였습니다. 

    ![Paper_3]({{ "/images/sangmin/paper_3.png" | prepend: site.baseurl }})

* Anomaly Score가 Threshold를 넘어서게 되면 이상이라고 판단을 합니다.

* 논문에서는 기존의 여러 방법들을 적용해 보았지만 LSTM-VAE모델의 성능이 가장 좋았다고 합니다.
