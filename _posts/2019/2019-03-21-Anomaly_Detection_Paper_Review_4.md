---
layout: post
title: "[Deep learning for anomaly detection in multivariate time series data] Paper Review"
author: "박상민"
date: 2019-03-22 19:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection, Detection Model]
---

본 포스트는 'Deep learning for anomaly detection in multivariate time series data' 논문을 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.
> 
> 아직 지식이 많이 부족하고, 경험이 부족하기 때문에, 고칠 것도 많을 것 같습니다. 고처야 할 부분은 언제든지 연락주시면 감사하겠습니다 :)

#  개요

이번글은 간략하게 읽은 여러 논문 중 네 번째 논문에 대해 정리한 글 입니다. 

논문을 조사하고 읽은 목적은 다른 곳에서는 어떤식으로 데이터를 구축하는지, 어떤 문제를 해결하려고 하였는지, 모델 성능평가는 어떻게 하는지, 어떤 방법으로 연구하는지 등의 인사이트를 얻기 위해 간단하게 조사한 것 입니다. 논문 중 꼭 자세히 읽어야 하는  부분은 좀 더 자세히 읽고, 개별 포스트를 만들어 정리하였습니다.
    
아래는 제가 읽은 논문들 중 10개에 대해서 간단하게 분류한 것 입니다.  
![Paper]({{ "/images/2019/paper_1.png" | prepend: site.baseurl }})

위 사진을 보면 어떤 논문이 어떤 모델을 썼는지, 시계열 데이터 사용 유무 등을 한번에 볼 수 있습니다. 예를들어 5번 논문의 경우 시게열 데이터를 사용했고, SVM 모델을 사용했습니다. 원이 겹쳐져있는 경우는 두 개를 같이 사용했다는 뜻 입니다. 즉, 5번 논문은 SVM모델과 DNN + LSTM를 동시에 사용한 모델이라는 뜻 입니다.

번역을 잘못하거나, 잘못 이해한 부분이 있다면 언제든지 말씀해주시면 반영하도록 하겠습니다!!


# 4. Deep learning for anomaly detection in multivariate time series data [4](https://users.informatik.haw-hamburg.de/~ubicomp/arbeiten/master/assendorp.pdf)

* 본 글은 자신들이 연구한 연구내용만 있는 것이 아니라, 머신러닝/딥러닝 기반의 다양한 이상감지 기법들의 내용이 포함되어 있습니다. 꼭 읽어보시면 좋을 것 같습니다.

* 기계 장치들에서 비정상적인 활동을 감지하는 것은 기계 부품에 손상을 줄 수 있는 고장을 방지하는 중요한 작업이라고 합니다.

* 지금까지의 모니터링 시스템은 도메인 지식이 풍부한 도메인 전문가가 있어야 하며, 이는 비용이 많이 든다고 말합니다.

* 글에서는 최근 많은 연구들에서 보듯이, 딥러닝은 다변수, 시계열 데이터에서 강력한 이상감지 능력을 보여주었다고 하고 있습니다.

* 딥러닝을 적용하게되면, 도메인 전문가가 하던 feature 엔지니어링 작업을 최소한으로 줄일 수 있기 때문에 많은 비용을 줄일 수 있다고 합니다.

* 본 글에서는 세탁기의 다변수 + 시계열 데이터를 사용하여 Autoencoder-base와 GAN-base의 이상감지를 비교하였습니다.