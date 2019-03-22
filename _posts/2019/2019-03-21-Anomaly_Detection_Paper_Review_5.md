---
layout: post
title: "[Anomaly Detection for a Water Treatment System Using Unsupervised Machine Learning] Paper Review"
author: "박상민"
date: 2019-03-21 19:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection, SVM]
---

본 포스트에는 CPS시스템에 딥러닝(DNN + LSTM) 모델과 SVM모델을 적용한 논문을 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.
> 
> 아직 지식이 많이 부족하고, 경험이 부족하기 때문에, 고칠 것도 많을 것 같습니다. 고처야 할 부분은 언제든지 연락주시면 감사하겠습니다 :)

#  개요

이번글은 간략하게 읽은 여러 논문 중 다섯 번째 논문에 대해 정리한 글 입니다. 

논문을 조사하고 읽은 목적은 다른 곳에서는 어떤식으로 데이터를 구축하는지, 어떤 문제를 해결하려고 하였는지, 모델 성능평가는 어떻게 하는지, 어떤 방법으로 연구하는지 등의 인사이트를 얻기 위해 간단하게 조사한 것 입니다. 논문 중 꼭 자세히 읽어야 하는  부분은 좀 더 자세히 읽고, 개별 포스트를 만들어 정리하였습니다.
    
아래는 제가 읽은 논문들 중 10개에 대해서 간단하게 분류한 것 입니다.  
![Paper]({{ "/images/2019/paper_1.png" | prepend: site.baseurl }})

위 사진을 보면 어떤 논문이 어떤 모델을 썼는지, 시계열 데이터 사용 유무 등을 한번에 볼 수 있습니다. 예를들어 5번 논문의 경우 시게열 데이터를 사용했고, SVM 모델을 사용했습니다. 원이 겹쳐져있는 경우는 두 개를 같이 사용했다는 뜻 입니다. 즉, 5번 논문은 SVM모델과 DNN + LSTM를 동시에 사용한 모델이라는 뜻 입니다.

번역을 잘못하거나, 잘못 이해한 부분이 있다면 언제든지 말씀해주시면 반영하도록 하겠습니다!!


# 5. Anomaly Detection for a Water Treatment System Using Unsupervised Machine Learning [5](https://arxiv.org/pdf/1709.05342.pdf)

* CPS(Cyber-Physical System)는 물리적 프로세서와 상호작용하는 컴퓨팅 요소로 구성된 복잡한 시스템입니다.

* CPS에서는 제어요소, 네트워크 또는 물리적 공격으로 이상현상이 일어날 수 있다고 논문에서는 말합니다.

* 본 논문에서는 CPS상의 이상을 감지하는 방법에 대해서 두 가지의 비지도학습 방안을 제안하였고, CPS시스템에 적용하였습니다.

* 두 가지 방안은 LSTM layer가 있는 DNN 네트워크와 SVM을 사용하는 방안입니다.

* 실제로 적용해보니, DNN 네트워크가 Precision과 F-score가 더 높았고, SVM이 Recall이 더 높았다고 말말합니다.

    ![Paper_5]({{ "/images/2019/paper_5.png" | prepend: site.baseurl }})

* 하지만 DNN네트워크는 학습에 2주가 걸렸고, SVM은 30분이 걸렸다고 설명합니다.

* 두 가지 방법모두 센서 값의 점진적인 변화를 탐지 못하는 한계점도 있었다고 논문에서는 밝힙니다.