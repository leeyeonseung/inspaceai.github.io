---
layout: post
title: "[LSTM-based Encoder-Decoder for Multi-sensor Anomaly Detection] Paper Review"
author: "박상민"
date: 2019-03-22 15:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection, LSTM-Encoder-Decoder]
---

본 포스트는 기계 장치 센서에 딥러닝 기반 이상감지 모델을 적용한 논문에 대해 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.


# 8. LSTM-based Encoder-Decoder for Multi-sensor Anomaly Detection [8](https://arxiv.org/pdf/1607.00148.pdf)

* 엔진, 차량, 항공기 등과 같은 기계 장치에는 일반적으로 기계의 상태나 동작을 캡처하는 수많은 센서가 있습니다. 그러나 종종 센서에 포착 되지 않는 외부요인, 변수들이 많으며, 이는 본질적으로 예측할 수 없는 시계열 데이터로 이어집니다. 
    * EX) 수동 제어, 모니터링 되지 않는 환경과 조건 등

* 이러한 상황에서 수학에 의존하는 모델을 사용하는 것은 어렵다고 논문에서는 기존 이상감지 방식의 한게점을 말하고 있습니다.

* 본 논문에서는 정상 데이터를 학습 후 reconstruction error를 이용해 이상감지를 하는 LSTM-based Encoder-Decoder Anomaly detection을 제안합니다.

* EncDec-AD를 통하여 예측가능한, 예측불가능한, 주기적인, 불규칙적인, 준 주기적인 시계열데이터에서 이상징후를 할 수 있으며, 짧은 주기(30)의 시계열과 굉장히 긴 주기의 시계열(500)에서도 이상징후를 감지할 수 있다고 말하고 있습니다.

* 논문에서는 전력수요, 우주 왕복선, ECG, 그리고 2개의 real-world 엔진 데이터 셋을 이용해 실험을 진행하였다고 합니다.

    ![Paper_8]({{ "/images/sangmin/paper_8.PNG" | prepend: site.baseurl }})

    * 위 사진에서 첫 번째 열은 정상데이터, 두 번째 열은 비정상 데이터입니다.
    * 1행(파란색 plot)은 실제 원본 데이터입니다.
    * 2행(초록색 plot)은 모델의 reconstructed sequences 입니다.
    * 3행(빨간색 plot)은 anomaly score 입니다.