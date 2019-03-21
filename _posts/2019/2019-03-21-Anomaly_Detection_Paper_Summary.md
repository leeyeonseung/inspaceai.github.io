---
layout: post
title: "머신러닝 기반 이상감지 연구 논문 리뷰"
author: "박상민"
date: 2019-03-21 18:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection, Time Series Data]
---

본 포스트에서는 머신러닝 기반 이상감지 모델을 연구한 9개의 논문에 대해 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.
> 
> 아직 지식이 많이 부족하고, 경험이 부족하기 때문에, 고칠 것도 많을 것 같습니다. 고처야 할 부분은 언제든지 연락주시면 감사하겠습니다 :)

#  개요

이번글은 읽었던 여러 논문 중 간략하게 읽은 9개의 논문에 대한 정리 글 입니다. 

논문을 조사하고 읽은 목적은 다른 곳에서는 어떤식으로 데이터를 구축하는지, 어떤 문제를 해결하려고 하였는지, 모델 성능평가는 어떻게 하는지, 어떤 방법으로 연구하는지 등의 인사이트를 얻기 위해 간단하게 조사한 것 입니다. 논문 중 꼭 자세히 읽어야 하는  부분은 좀 더 자세히 읽고, 개별 포스트를 만들어 정리하였습니다.
    
아래는 제가 읽은 논문들 중 10개에 대해서 간단하게 분류한 것 입니다.  
![Paper]({{ "/images/2019/paper_1.png" | prepend: site.baseurl }})

위 사진을 보면 어떤 논문이 어떤 모델을 썼는지, 시계열 데이터 사용 유무 등을 한번에 볼 수 있습니다. 예를들어 5번 논문의 경우 시게열 데이터를 사용했고, SVM 모델을 사용했습니다. 원이 겹쳐져있는 경우는 두 개를 같이 사용했다는 뜻 입니다. 즉, 5번 논문은 SVM모델과 DNN + LSTM를 동시에 사용한 모델이라는 뜻 입니다.

번역을 잘못하거나, 잘못 이해한 부분이 있다면 언제든지 말씀해주시면 반영하도록 하겠습니다!!

# 논문 요약 정리

# 1. Applications of Deep Learning Neural Networks to Satellite Telemetry Monitoring [1](https://elib.dlr.de/121211/1/6.2018-2558.pdf)

기존의 자동원격모니터링 시스템은 이상위험을 감지하지 못한다고 저자는 말합니다. 
그래서 본 논문에서는 새로운 3개의 Application을 제안합니다.

* Autoencoder(오토인코더)
    * 오토인코더 모델을 이용한 자동 피쳐 추출
    * 오토인코더 모델을 이용한 이상감지
* Multi LSTM-Layer
    * 예측 모델을 이용하여 4시간 30분 후의 Telemetry value를 예측 -> 이상 예측

False Positive를 줄이고, 다양한 형태의 이상을 감지하였다고 논문에서는 밝힙니다.

# 2. Performance assessment of NOSTRADAMUS & other machine learning-based telemetry monitoring systems on a spacecraft anomalies database [2](https://arc.aiaa.org/doi/pdf/10.2514/6.2018-2559)

* 최근 몇년동안 머신러닝을 이용한 새로운 탐지방법들이 제안되었다고 말하고 있습니다.

* 저자는 여러개의 이상감지 방법들을 정량적으로 비교할 때 얻은 평가방법론과 결과를 제시하고자 하였습니다.

* 저자는 머신러닝 모델을 학습하는 방향(방법)이 성능 향상에 큰 영향을 미치지 않았다는 것을 강조합니다.

* 데이터의 전처리가 결과에 많은 영향을 주었다고 합니다.

* 머신러닝에서 가장 중요한 작업은 데이터의 이해, 문제정의, 최적의 방법찾기라고 논문에서는 말합니다.

* 논문에서는 머신러닝 모델의 성능만 중요한게 아니라, 결과의 해석 가능성, 처리시간(계산 시간), 새로운 데이터에 시스템 업데이트 유무라고 밝힙니다.

# 3. A Multimodal Anomaly Detector for Robot-Assisted Feeding Using an LSTM-based Variational Autoencoder [3](https://arxiv.org/pdf/1711.00614.pdf)

* 본 논문의 동기는 밥을 먹는데 도와주는 로봇이 구조적, 하드웨어적 문제로 종종 오류가 발생해서 발생한 오류(이상)들을 감지하는 시스템을 개발하는 것이었습니다.

* 구조적, 하드웨어적 이상들을 감지하는 시스템이 없다면 로봇이 자주 고장나게 되고, 수리비용이 높아지며, 사용자들이 더 이상 사용하지 않을 수 있는 문제점이 있다고 합니다.

* 비정상적인 이상 상황들을 검출하고, 인식한다면 미리 예방이 가능하다고 논문에서는 말하고 있습니다.

* LSTM-VAE(LSTM based variational autoencoder)를 이용해 Anomaly Score를 계산하였습니다. 

    ![Paper_3]({{ "/images/2019/paper_3.png" | prepend: site.baseurl }})

* Anomaly Score가 Threshold를 넘어서게 되면 이상이라고 판단을 합니다.

* 논문에서는 기존의 여러 방법들을 적용해 보았지만 LSTM-VAE모델의 성능이 가장 좋았다고 합니다.

# 4. Deep learning for anomaly detection in multivariate time series data [4](https://users.informatik.haw-hamburg.de/~ubicomp/arbeiten/master/assendorp.pdf)

* 본 글은 자신들이 연구한 연구내용만 있는 것이 아니라, 머신러닝/딥러닝 기반의 다양한 이상감지 기법들의 내용이 포함되어 있습니다. 꼭 읽어보시면 좋을 것 같습니다.

* 기계 장치들에서 비정상적인 활동을 감지하는 것은 기계 부품에 손상을 줄 수 있는 고장을 방지하는 중요한 작업이라고 합니다.

* 지금까지의 모니터링 시스템은 도메인 지식이 풍부한 도메인 전문가가 있어야 하며, 이는 비용이 많이 든다고 말합니다.

* 글에서는 최근 많은 연구들에서 보듯이, 딥러닝은 다변수, 시계열 데이터에서 강력한 이상감지 능력을 보여주었다고 하고 있습니다.

* 딥러닝을 적용하게되면, 도메인 전문가가 하던 feature 엔지니어링 작업을 최소한으로 줄일 수 있기 때문에 많은 비용을 줄일 수 있다고 합니다.

* 본 글에서는 세탁기의 다변수 + 시계열 데이터를 사용하여 Autoencoder-base와 GAN-base의 이상감지를 비교하였습니다.

# 5. Anomaly Detection for a Water Treatment System Using Unsupervised Machine Learning [5](https://arxiv.org/pdf/1709.05342.pdf)

* CPS(Cyber-Physical System)는 물리적 프로세서와 상호작용하는 컴퓨팅 요소로 구성된 복잡한 시스템입니다.

* CPS에서는 제어요소, 네트워크 또는 물리적 공격으로 이상현상이 일어날 수 있다고 논문에서는 말합니다.

* 본 논문에서는 CPS상의 이상을 감지하는 방법에 대해서 두 가지의 비지도학습 방안을 제안하였고, CPS시스템에 적용하였습니다.

* 두 가지 방안은 LSTM layer가 있는 DNN 네트워크와 SVM을 사용하는 방안입니다.

* 실제로 적용해보니, DNN 네트워크가 Precision과 F-score가 더 높았고, SVM이 Recall이 더 높았다고 말말합니다.

    ![Paper_5]({{ "/images/2019/paper_5.png" | prepend: site.baseurl }})

* 하지만 DNN네트워크는 학습에 2주가 걸렸고, SVM은 30분이 걸렸다고 설명합니다.

* 두 가지 방법모두 센서 값의 점진적인 변화를 탐지 못하는 한계점도 있었다고 논문에서는 밝힙니다.

# 6. Long Short Term Memory Networks for Anomaly Detection in Time Series [6](https://www.elen.ucl.ac.be/Proceedings/esann/esannpdf/es2015-56.pdf)

* 기존의 모니터링 방식은 통계적 방식을 이용하지만, time window 매개변수를 미리 지정해줘야 하며, 이는 결과에 큰 영향을 끼친다고 합니다.

* LSTM 네트워크는 window 사이즈를 지정해 줄 필요가 없으며, ‘memory cells’를 통해 vanishing gradient 문제를 해결하였다고 설명하고 있습니다.

* LSTM 네트워크는 장기 패턴이 있는 시퀀스를 학습하는데 매우 유용하며, 레이어를 쌓으면 더 높은 수준의 시간적인 특징을 학습할 수 있다고 설명하고 있습니다.

* 본 논문에서는 stacked LSTM 네트워크를 이용해 window를 정해주거나 전처리 없이 이상감지를 할 수 있음을 보여주었습니다.

* 데이터는 ECG, 우주 왕복선, 전력 수요, 엔진 센서 데이터 셋을 이용하였고, normal 데이터로 훈련을 하였다고 말하고 있습니다.

* Stacked 된 LSTM 네트워크는 좋은 성능을 보여주었고, RNN보다 LSTM 네트워크가 성능이 더 좋았다고 밝히고 있습니다.          

    ![Paper_6]({{ "/images/2019/paper_6.PNG" | prepend: site.baseurl }})

# 7. Anomaly Detection with Generative Adversarial Networks for Multivariate Time Series [7](https://arxiv.org/pdf/1709.05342.pdf)

* 오늘날 CPS 시스템은 크고, 복잡하며, 사이버 공격의 목표가 되는 network sensor와 actuators가 부착되어 있다고 눈문에서는 설명합니다.

* 기존의 이상감지 기법 들은 역동적이고, 복잡한 것 들을 감지할 수 없다는 단점을 논문에서는 밝힙니다.

* 비지도학습(Unsupervised)기반의 머신러닝 기법을 이용해 비정상적인 동작을 공격으로 분류할 수 있다고 합니다.

* 본 논문에서는 복잡한 네트워크를 위한 새로운 Generative Adversarial Networks-based Anomaly Detection(GAN-AD) 방안을 제안하였습니다.

* GAN모델 내에있는 LSTM-RNN이 다변수 시계열 데이터의 분포를 capture합니다.

* 각 센서와 액추에이터 시계열 데이터를 독립적으로 처리하는 대신, 시계열 데이터를 동시에 모델링하여 잠재적인 상호작용을 고려한다고 설명합니다.

* Secure Water Treatment Testbed(SWaT) 데이터 셋을 사용해 테스트를 하였으며, 다른 비지도학습 이상감지 기법보다 성능이 좋았다고 말하고 있습니다.

    ![Paper_7]({{ "/images/2019/paper_7.png" | prepend: site.baseurl }})

# 8. LSTM-based Encoder-Decoder for Multi-sensor Anomaly Detection [8](https://arxiv.org/pdf/1607.00148.pdf)

* 엔진, 차량, 항공기 등과 같은 기계 장치에는 일반적으로 기계의 상태나 동작을 캡처하는 수많은 센서가 있습니다. 그러나 종종 센서에 포착 되지 않는 외부요인, 변수들이 많으며, 이는 본질적으로 예측할 수 없는 시계열 데이터로 이어집니다. 
    * EX) 수동 제어, 모니터링 되지 않는 환경과 조건 등

* 이러한 상황에서 수학에 의존하는 모델을 사용하는 것은 어렵다고 논문에서는 기존 이상감지 방식의 한게점을 말하고 있습니다.

* 본 논문에서는 정상 데이터를 학습 후 reconstruction error를 이용해 이상감지를 하는 LSTM-based Encoder-Decoder Anomaly detection을 제안합니다.

* EncDec-AD를 통하여 예측가능한, 예측불가능한, 주기적인, 불규칙적인, 준 주기적인 시계열데이터에서 이상징후를 할 수 있으며, 짧은 주기(30)의 시계열과 굉장히 긴 주기의 시계열(500)에서도 이상징후를 감지할 수 있다고 말하고 있습니다.

* 논문에서는 전력수요, 우주 왕복선, ECG, 그리고 2개의 real-world 엔진 데이터 셋을 이용해 실험을 진행하였다고 합니다.

    ![Paper_8]({{ "/images/2019/paper_8.png" | prepend: site.baseurl }})

    > 위 사진에서 첫 번째 열은 정상데이터, 두 번째 열은 비정상 데이터입니다.
    > 1행(파란색 plot)은 실제 원본 데이터입니다.
    > 2행(초록색 plot)은 모델의 reconstructed sequences 입니다.
    > 3행(빨간색 plot)은 anomaly score 입니다.

# 9. Time Series Anomaly Detection [9](https://arxiv.org/ftp/arxiv/papers/1708/1708.03665.pdf)

* 구글의 실시간 트래픽 데이터에서 이상을 감지하기 위해서 연구를 시작하였다고 논문에서는 밝힙니다.

* 데이터는 노이즈가 있고, 트래픽 패턴이 있는 주기적인 데이터에서 이상을 감지하기위해 머신러닝 기법과 통계적 기법으로 접근하였다고 합니다.

* 많은 양의 라벨된 데이터가 없기 때문에 지도학습(supervised)의 분류 문제로 접근할 수 없었으므로, 두 부분으로 문제에 접근하였다고 하는데 다음과 같습니다.

    * 첫 번째는, regression과 시계열 데이터에서 값을 예측하기위해 텐서플로우를 이용하여 DNN, RNN, LSTM을 포함한 다양한 모델을 학습시킨 것 것 입니다.

    * 두 번째는, 실제 값과 예측값을 비교하는 anomaly rule(이상탐지 규칙)을 만들어 비교한 것 입니다.

* 논문에서는 두 개의 이상탐지 규칙은 트래픽 데이터가 잠시 지연되거나, 일시적으로 값이 튀는 것보다 지속적인 이상(sustained anomalies)를 찾는 문제에 더 초점을 두었다고 설명합니다.

* 모든 모델의 결과를 분석해 보니 논문에서 사용한 이상탐지 규칙이 효과적이었다고 밝히고 있습니다.

* 논문에서는 모델과 규칙들을 여러가지 조합으로 실험을 진행하였는데, 두 개의 규칙의 교차점을 사용하면 거의 모든 모델에서 이상을 찾아낼 수 있었다고 합니다.

* 통계적인 베이스가 있는 이상감지 규칙과, 사용자가 반복적으로 false positive를 수동으로 제거할 수 있도록 쉽게 수정할 수 있는 규칙은 이상징후를 탐지할 수 있는 매우 강력한 방법이라고 말하고 있습니다.

    ![Paper_9]({{ "/images/2019/paper_9.png" | prepend: site.baseurl }})

