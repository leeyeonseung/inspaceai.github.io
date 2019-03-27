---
layout: post
title: "[Applications of Deep Learning Neural Networks to Satellite Telemetry Monitoring] Paper Review"
author: "박상민"
date: 2019-03-21 19:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection]
---

본 포스트는 'Applications of Deep Learning Neural Networks to Satellite Telemetry Monitoring' 논문을 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.

# 1. Applications of Deep Learning Neural Networks to Satellite Telemetry Monitoring [1](https://elib.dlr.de/121211/1/6.2018-2558.pdf)

기존의 자동원격모니터링 시스템은 이상위험을 감지하지 못한다고 저자는 말합니다. 
그래서 본 논문에서는 새로운 3개의 Application을 제안합니다.

* Autoencoder(오토인코더)
    * 오토인코더 모델을 이용한 자동 피쳐 추출
    * 오토인코더 모델을 이용한 이상감지
* Multi LSTM-Layer
    * 예측 모델을 이용하여 4시간 30분 후의 Telemetry value를 예측 -> 이상 예측

False Positive를 줄이고, 다양한 형태의 이상을 감지하였다고 논문에서는 밝힙니다.