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

# 6. Long Short Term Memory Networks for Anomaly Detection in Time Series [6](https://www.elen.ucl.ac.be/Proceedings/esann/esannpdf/es2015-56.pdf)

* 기존의 모니터링 방식은 통계적 방식을 이용하지만, time window 매개변수를 미리 지정해줘야 하며, 이는 결과에 큰 영향을 끼친다고 합니다.

* LSTM 네트워크는 window 사이즈를 지정해 줄 필요가 없으며, ‘memory cells’를 통해 vanishing gradient 문제를 해결하였다고 설명하고 있습니다.

* LSTM 네트워크는 장기 패턴이 있는 시퀀스를 학습하는데 매우 유용하며, 레이어를 쌓으면 더 높은 수준의 시간적인 특징을 학습할 수 있다고 설명하고 있습니다.

* 본 논문에서는 stacked LSTM 네트워크를 이용해 window를 정해주거나 전처리 없이 이상감지를 할 수 있음을 보여주었습니다.

* 데이터는 ECG, 우주 왕복선, 전력 수요, 엔진 센서 데이터 셋을 이용하였고, normal 데이터로 훈련을 하였다고 말하고 있습니다.

* Stacked 된 LSTM 네트워크는 좋은 성능을 보여주었고, RNN보다 LSTM 네트워크가 성능이 더 좋았다고 밝히고 있습니다.          

    ![Paper_6]({{ "/images/sangmin/paper_6.PNG" | prepend: site.baseurl }})