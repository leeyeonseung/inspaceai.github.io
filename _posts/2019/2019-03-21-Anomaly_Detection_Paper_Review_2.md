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
> 
> 아직 지식이 많이 부족하고, 경험이 부족하기 때문에, 고칠 것도 많을 것 같습니다. 고처야 할 부분은 언제든지 연락주시면 감사하겠습니다 :)

#  개요

이이번글은 간략하게 읽은 여러 논문 중 두 번째 논문에 대해 정리한 글 입니다. 

논문을 조사하고 읽은 목적은 다른 곳에서는 어떤식으로 데이터를 구축하는지, 어떤 문제를 해결하려고 하였는지, 모델 성능평가는 어떻게 하는지, 어떤 방법으로 연구하는지 등의 인사이트를 얻기 위해 간단하게 조사한 것 입니다. 논문 중 꼭 자세히 읽어야 하는  부분은 좀 더 자세히 읽고, 개별 포스트를 만들어 정리하였습니다.
    
아래는 제가 읽은 논문들 중 10개에 대해서 간단하게 분류한 것 입니다.  
![Paper]({{ "/images/2019/paper_1.png" | prepend: site.baseurl }})

위 사진을 보면 어떤 논문이 어떤 모델을 썼는지, 시계열 데이터 사용 유무 등을 한번에 볼 수 있습니다. 예를들어 5번 논문의 경우 시게열 데이터를 사용했고, SVM 모델을 사용했습니다. 원이 겹쳐져있는 경우는 두 개를 같이 사용했다는 뜻 입니다. 즉, 5번 논문은 SVM모델과 DNN + LSTM를 동시에 사용한 모델이라는 뜻 입니다.

번역을 잘못하거나, 잘못 이해한 부분이 있다면 언제든지 말씀해주시면 반영하도록 하겠습니다!!


# 2. Performance assessment of NOSTRADAMUS & other machine learning-based telemetry monitoring systems on a spacecraft anomalies database [2](https://arc.aiaa.org/doi/pdf/10.2514/6.2018-2559)

* 최근 몇년동안 머신러닝을 이용한 새로운 탐지방법들이 제안되었다고 말하고 있습니다.

* 저자는 여러개의 이상감지 방법들을 정량적으로 비교할 때 얻은 평가방법론과 결과를 제시하고자 하였습니다.

* 저자는 머신러닝 모델을 학습하는 방향(방법)이 성능 향상에 큰 영향을 미치지 않았다는 것을 강조합니다.

* 데이터의 전처리가 결과에 많은 영향을 주었다고 합니다.

* 머신러닝에서 가장 중요한 작업은 데이터의 이해, 문제정의, 최적의 방법찾기라고 논문에서는 말합니다.

* 논문에서는 머신러닝 모델의 성능만 중요한게 아니라, 결과의 해석 가능성, 처리시간(계산 시간), 새로운 데이터에 시스템 업데이트 유무라고 밝힙니다.