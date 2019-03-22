---
layout: post
title: "[Long Short Term Memory Networks for Anomaly Detection in Time Series] Paper Review"
author: "박상민"
date: 2019-03-22 19:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection, LSTM]
---

본 포스트는 LSTM 네트워크를 이용해 이상감지 모델을 적용한 논문을 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.
> 
> 아직 지식이 많이 부족하고, 경험이 부족하기 때문에, 고칠 것도 많을 것 같습니다. 고처야 할 부분은 언제든지 연락주시면 감사하겠습니다 :)

#  개요

이번글은 간략하게 읽은 여러 논문 중 여섯 번째 논문에 대해 정리한 글 입니다. 

논문을 조사하고 읽은 목적은 다른 곳에서는 어떤식으로 데이터를 구축하는지, 어떤 문제를 해결하려고 하였는지, 모델 성능평가는 어떻게 하는지, 어떤 방법으로 연구하는지 등의 인사이트를 얻기 위해 간단하게 조사한 것 입니다. 논문 중 꼭 자세히 읽어야 하는  부분은 좀 더 자세히 읽고, 개별 포스트를 만들어 정리하였습니다.
    
아래는 제가 읽은 논문들 중 10개에 대해서 간단하게 분류한 것 입니다.  
![Paper]({{ "/images/2019/paper_1.png" | prepend: site.baseurl }})

위 사진을 보면 어떤 논문이 어떤 모델을 썼는지, 시계열 데이터 사용 유무 등을 한번에 볼 수 있습니다. 예를들어 5번 논문의 경우 시게열 데이터를 사용했고, SVM 모델을 사용했습니다. 원이 겹쳐져있는 경우는 두 개를 같이 사용했다는 뜻 입니다. 즉, 5번 논문은 SVM모델과 DNN + LSTM를 동시에 사용한 모델이라는 뜻 입니다.

번역을 잘못하거나, 잘못 이해한 부분이 있다면 언제든지 말씀해주시면 반영하도록 하겠습니다!!


# 6. Long Short Term Memory Networks for Anomaly Detection in Time Series [6](https://www.elen.ucl.ac.be/Proceedings/esann/esannpdf/es2015-56.pdf)

* 기존의 모니터링 방식은 통계적 방식을 이용하지만, time window 매개변수를 미리 지정해줘야 하며, 이는 결과에 큰 영향을 끼친다고 합니다.

* LSTM 네트워크는 window 사이즈를 지정해 줄 필요가 없으며, ‘memory cells’를 통해 vanishing gradient 문제를 해결하였다고 설명하고 있습니다.

* LSTM 네트워크는 장기 패턴이 있는 시퀀스를 학습하는데 매우 유용하며, 레이어를 쌓으면 더 높은 수준의 시간적인 특징을 학습할 수 있다고 설명하고 있습니다.

* 본 논문에서는 stacked LSTM 네트워크를 이용해 window를 정해주거나 전처리 없이 이상감지를 할 수 있음을 보여주었습니다.

* 데이터는 ECG, 우주 왕복선, 전력 수요, 엔진 센서 데이터 셋을 이용하였고, normal 데이터로 훈련을 하였다고 말하고 있습니다.

* Stacked 된 LSTM 네트워크는 좋은 성능을 보여주었고, RNN보다 LSTM 네트워크가 성능이 더 좋았다고 밝히고 있습니다.          

    ![Paper_6]({{ "/images/2019/paper_6.PNG" | prepend: site.baseurl }})