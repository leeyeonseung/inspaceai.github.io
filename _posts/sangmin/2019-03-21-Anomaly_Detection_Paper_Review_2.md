---
layout: post
title: "[Performance assessment of NOSTRADAMUS & other machine learning-based telemetry monitoring systems on a spacecraft anomalies database] Paper Review"
author: "박상민"
date: 2019-03-22 19:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection]
---

본 포스트는 'Performance assessment of NOSTRADAMUS & other machine learning-based telemetry monitoring systems on a spacecraft anomalies database' 논문을 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.


# 2. Performance assessment of NOSTRADAMUS & other machine learning-based telemetry monitoring systems on a spacecraft anomalies database [2](https://arc.aiaa.org/doi/pdf/10.2514/6.2018-2559)

* 최근 몇년동안 머신러닝을 이용한 새로운 탐지방법들이 제안되었다고 말하고 있습니다.

* 저자는 여러개의 이상감지 방법들을 정량적으로 비교할 때 얻은 평가방법론과 결과를 제시하고자 하였습니다.

* 저자는 머신러닝 모델을 학습하는 방향(방법)이 성능 향상에 큰 영향을 미치지 않았다는 것을 강조합니다.

* 데이터의 전처리가 결과에 많은 영향을 주었다고 합니다.

* 머신러닝에서 가장 중요한 작업은 데이터의 이해, 문제정의, 최적의 방법찾기라고 논문에서는 말합니다.

* 논문에서는 머신러닝 모델의 성능만 중요한게 아니라, 결과의 해석 가능성, 처리시간(계산 시간), 새로운 데이터에 시스템 업데이트 유무라고 밝힙니다.