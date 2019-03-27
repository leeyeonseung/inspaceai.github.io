---
layout: post
title: "[A Data-Driven Health Monitoring Method for Satellite Housekeeping Data Based on Probabilistic Clustering and Dimensionality Reduction] Paper Review"
author: "박상민"
date: 2019-03-22 19:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection, Telemetry]
---

본 포스트는 Spacecraft Telemetry 데이터의 특징 분석과 Anomaly Score 모델을 적용한 논문을 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.


# 11. A Data-Driven Health Monitoring Method for Satellite Housekeeping Data Based on Probabilistic Clustering and Dimensionality Reduction [11](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=7859276)

![Paper_11]({{ "/images/sangmin/paper_11_1.png" | prepend: site.baseurl }})

> 'A Data-Driven Health Monitoring Method for Satellite Housekeeping Data Based on Probabilistic Clustering and Dimensionality Reduction' 논문입니다.
>
> JAXA와 도쿄대학교에서 작성한 논문입니다. 인공위성 Telemetry 데이터를 사용하였습니다.
>
> 위성 Telemetry의 특징 분석, 전처리 기법등을 위주로 읽어보았습니다.

## 논문 요약

* 인공위성 운영에 있어서 시스템의 상태를 모니터링하고, 이상징후를 감지하는 것은 매우 중요하다.
* 최근에는 과거에 수집 된 많은 양의 측정 데이터에 적용되는 데이터 중심 접근법이 주목을 받고 있다.
* 본 논문에서는 데이터 기반의 새로운 모니터링 방법과 이상 검출 방안을 제안한다.
* 새로운 방법은 probabilistic 차원축소 및 클러스터링 기반이다.
* 일본 항공우주국의 소형 시범위성 Telemetry에 적용, 평가하였다.
* 고차원, Multimodality 등의 특성을 가지고있는 위성 Telemetry에 적합하다.
* Anomaly score, 클러스터 결과 등을 운영자에게 정보 제공한다.
* 위성의 인공 Telemetry에 2년 이상 적용해 검증 받았다.
* 본 연구를 바탕으로 space craft에 대한 범용적인 모니터링 시스템 개발할 예정이다.

논문에서는 데이터를 머신러닝 모델에 적용하기 전에 데이터의 특성을 이해하는게 중요하다고 말합니다.

## 위성 Telemetry의 6가지 특성

* High Dimensionality (고차원)
* Multimodality (복합성)
* Heterogeneous (이질성)
* Temporal Dependence (시간 종속성)
* Missing Data (누락 데이터)
* Trivial Outliers (사소한 이상치들)

## 위성 Telemetry 분석

위성 Telemetry를 다음과 같이 분석했습니다.

### High Dimensionality (고차원)

* 위성의 Telemetry 데이터는 고차원이다.
* 변수가 수백 ~ 수천개에 이른다.
* 데이터 샘플 간의 거리를 정확하게 측정하지 못한다.
* 위와 같은 문제들을 차원의 저주라고 한다.
* 간단한 거리기반의 이상감지 알고리즘은 인공위성의 Telemetry 데이터에 적합하지 않다.
* 위성 Telemetry 데이터들은 서로 강하게 연관되어 있으므로, 실질적인 차원은 훨씬 낮다.

### Multimodality (복합성)

* 위성 시스템은 여러 가지의 동작 모드들을 가지고있다. 
* 시간에 따라 모드가 바뀌기도 한다.
* 지구궤도위성의 기본적인 모드는 낮과 밤이 바뀌는 모드이다.
* 이 두개의 모드 사이에서는 발전량 또는 표면적인 온도의 뚜렷한 차이가 있다.
* 결과적으로 위성의 Telemetry 데이터의 분포는 Multimodal이 되고, 샘플은 데이터 공간에서 다중 클러스터로 구성된다.=

### Heterogeneous (이질성)
* 위성 Telemetry 데이터는 두 가지 타입으로 나뉘어진다.
* 실제 값을 갖는 continuous한 변수
    * Ex)온도 등의 센서 값, 전력 값

* 범주형(categorical) 값을 갖는 이산형 변수
    * 정수로만 되어있음
    * Ex)낮과 밤, 어떤 모드들의 정수 값 등

### Temporal Dependence (시간 종속성)

* 인공위성 시스템은 동적 시스템이므로 다변수의 시계열 데이터이다.
* 시간적인 특징은 위성 Telemetry 데이터의 필수적인 속성이며, 모니터링에도 매우 유용하다.
* 여러 변수에서 값이 한 번에 변경되면 이벤트가 발생되었다고 볼 수 있다.
* 하지만, 이 연구에서는 trivial(사소한) outlier를 탐지하는데 초점을 맞추었다.

### Missing Data (누락 데이터)
* *논문에서도 실제로 'missing data'라고 표현을 하고 있어, 누락데이터라고 포현을 하였습니다. 하지만 여기서의 missing은 들어와야 할 데이터가 안들어오는 상황 보다는, 데이터의 샘플링 주기가 달라 비어있는 상황을 말합니다.*

* 대부분의 spacecraft 시스템에서는 샘플링 기간과 주기가 다르므로, 모든 변수의 값이 얻어지는 건 아니다.
* 자세, 각도 및 속도 등은 높은 샘플링 속도를 가지고 있고, 온도 등은 낮은 샘플링 속도를 가지고 있다.
* 위성 Telemetry 데이터의 대부분은 누락(missing)된다.
* 대부분의 머신러닝 알고리즘들은 기본적으로 데이터가 완벽하다고 생각한다.
* 위성 Telemetry 데이터를 머신러닝 모델에 적용할 때, 누락된 데이터를 처리할 수 있도록 수정하거나, 누락된 요소들을 미리 복구하기위한 전처리를 해주고, 학습 알고리즘에 제공해주는 작업이 필요하다.

* 아래사진은 논문에서 missing data의 missing 여부를 시각화 한 것입니다. 흰색은 누락된 부분이고, 검은색은 누락되지 않은 부분입니다.

![Paper_11]({{ "/images/sangmin/paper_11_2.png" | prepend: site.baseurl }})

### Trivial Outliers (사소한 이상치들)

* 위성 Telemetry 데이터에서는 가끔씩 굉장히 큰 이상데이터들이 데이터 변환 또는 전송오류로 생길 수도 있다.
![Paper_11]({{ "/images/sangmin/paper_11_3.png" | prepend: site.baseurl }})

* 위성 Telemetry 데이터에서는 가끔씩 굉장히 큰 이상데이터들이 데이터 변환 또는 전송오류로 생길 수도 있다는 것 이다.
* 중요한 점은 이러한 오류들(point)이 오직 데이터 변환 또는 전송 오류로만 인해서 발생하고, 심각한 이상징후를 나타내지 않는 것 이다.
* Trivial outlier는 심각한 오류와는 차별화되야 하며, 그 발견이 논문의 목적 중 하나
* Trivial outlier는 절대값이 굉장히 크기 때문에, 심각한 오류나 예외들의 값이 안보일 수 있다. (숨겨질 수도 있다)
* 훈련데이터에 매우 큰 값을 가진 trivial outlier들이 포함되면 학습 된 모델이 손상될 수 있다.

## 위성 Telemetry 전처리 

위성 Telemetry 데이터의 특징 중 일부는 데이터 전처리 단계에서 처리될 수 있고, 이러한 작업은 머신러닝에 적용하는 것을 더 쉽게 할 수 있도록 한다고 합니다.

* 전처리 방법은 다음과 같습니다.
    * Detection and Removal of Trivial Outliers
    * Missing value completion
    * Normalization 
    
### Detection and Removal of Trivial Outliers

* Trivial outlier 데이터들은 모델 학습과 테스트에서 데이터 기반 비정상 탐지를 방해한다.
* 2가지의 뚜렷한 성격이 있다.
    * 매우 드물게 갑작스럽게 발생
    * 그 값은 비슷한 시간에 있는 값들과 매우 다르다는 것

* Trivial outliers를 탐지하고, 제거하기 위한 수식입니다. 상한선과 하한선을 설정하고, 상하한선을 넘을 경우 제거합니다.
![Paper_11]({{ "/images/sangmin/paper_11_4.png" | prepend: site.baseurl }})

### Missing value completion

* 위성의 Telemetry 데이터는 변수들마다 샘플링 주기와 타이밍이 다르기 때문에 구조적으로 데이터 누락이 발생할 수 있다,
* 본 논문에서는 단순한 방법을 사용하였다.
* 각각의 누락된 값이 바로 앞의 값으로 대체되는 ‘piecewise constant interpolation’이라는 보간법을 사용하였다.
* 선형 및 다항식 보간과 같은 고급 방법을 선택하지 않은 이유는 노이즈에 영향을 받아 다른 변칙적인 값을 생성할 수 있기 때문이다.

### Normalization

* 위성의 Telemetry 데이터는 실제 단위와 변수의 범위 등이 다양하기 때문에, 일반적인 다변수로 보는 것은 무리가 있다.
* 범위를 변환하는 작업 등을 통해서 모든 Telemetry 데이터를 정규화해서 균일하게 사용할 수 있도록 하였다.
* Categorical(범주형) 변수의 값들은 각 변수 빈도를 내림차순으로 1씩 증가하는 값으로 대체한다.
    * Ex)’DIS’ / ‘ENA’ Telemetry가 각각 0.8, 0.2의 확률이라면 DIS는 1이고, ENA는 0이다.

## Anomaly Score 산출

논문에서는 Anomaly Score를 산출하는 방법의 대해서도 작성하였습니다. Anomlay Score를 모니터링 담당자에게 중요한 지표가 될 것이라고 하였습니다.  수식적으로 복잡하게 작성되어있습니다. __이현호__ 연구원께서 관련 부분을 이해하는데 많은 도움을 주셨습니다.

Anomaly Score는 내가 뽑은 데이터 샘플의 희귀한 정도를 수치화시켜 나타낸 것 입니다.(희귀할수록 score는 높아지게 됩니다.)  
![Paper_11]({{ "/images/sangmin/paper_11_5.PNG" | prepend: site.baseurl }})

Anomaly Score는 Gaussian Mixture Model를 사용하였습니다. 간단하게 방식에 대해 설명드리기 전에 Guassain Mixture Model의 대한 설명을 잠깐 드리고, anomaly score를 산출하는 방법에 대해 간단하게 설명하겠습니다.

GMM(Gaussian Mixture Model)은 데이터가 K개의 정규분포로부터 생성되었다고 보는 모델입니다.  

![Paper_11]({{ "/images/sangmin/paper_11_6.png" | prepend: site.baseurl }})

위 사진의 분포를 더 자세히보면 아래 사진과 같은 3개의 정규분포로 되어있는 걸 볼 수 있습니다.  

![Paper_11]({{ "/images/sangmin/paper_11_7.png" | prepend: site.baseurl }})
위 사진과 같이 GMM은 K개의 정규분포로 데이터가 생성되었다고 보는 모델입니다.  

아래사진처럼 2차원과 3차원에서도 가능합니다.  
![Paper_11]({{ "/images/sangmin/paper_11_8.png" | prepend: site.baseurl }})

아래와 같이 C1 ~ C6까지 총 6개의 클러스터링 된 굉장히 이상적인 데이터 분포가 있다고 생각을 해보겠습니다.  
![Paper_11]({{ "/images/sangmin/paper_11_12.png" | prepend: site.baseurl }})

각 클러스터의 데이터 샘플들의 개수는 다음과 같습니다.  
![Paper_11]({{ "/images/sangmin/paper_11_13.png" | prepend: site.baseurl }})  

각 클러스터들의 데이터 샘플 개수가 위의 사진과 같다면, 전체 데이터 중 하나의 데이터를 뽑았을 때 그 데이터의 클러스터를 뽑을 확률을 구해야합니다.  

![Paper_11]({{ "/images/sangmin/paper_11_14.png" | prepend: site.baseurl }})

만약 내가 C1에 속한 데이터를 하나 뽑았다면, 확률 p는 1/5일 것 입니다.  C6에 속한 데이터를 하나 뽑았다면, p는 1/40일 것 입니다. 즉 클러스터에 속한 데이터 샘플들의 개수가 적을수록 p는 낮아질 것 입니다.  
![Paper_11]({{ "/images/sangmin/paper_11_9.png" | prepend: site.baseurl }})

아까 구한 p의 -log를 계산합니다. -log를 씌우게 되면 값이 p가 1에 가까울수록, -log(p)는 0에 수렴합니다. 반대로 p가 0에 가까울수록, -log(p)는 무한대로 발산하게 됩니다.
![Paper_11]({{ "/images/sangmin/paper_11_10.png" | prepend: site.baseurl }})

아래 사진과 같이 p확률을 구하고, -log(p)를 계산하면 우리가 원하는 anomaly score가 나오게 됩니다. p가 낮을 수록, score는 높아지게 되는 것이고, 이는 내가 뽑은 하나의 데이터가 속한 클러스터에서 그 클러스터에 속한 데이터 개수가 적을수록, p는 높아질 것이고, score도 높아진다는 것 입니다.  
![Paper_11]({{ "/images/sangmin/paper_11_11.png" | prepend: site.baseurl }})

## Conclusion

본 논문에서 제안한 데이터 기반 이상감지 모니터링 시스템은 고차원, Multimodality 등의 특징을 가진 위성 Telemetry에 적합하다. 모니터링 운영자는 본 모델을 이용해 시스템의 상태를 파악하는데 많은 도움이 될 것이다.

2년 이상 실제 인공 위성 Telemetry 데이터에 적용하여 본 모델을 검증하였고, 타당성을 입증한 것은 굉장히 중요한 성과다. 본 연구에서 얻은 경험을 바탕으로 spacecraft에 범용적으로 적용할 수 있는 모니터링 시스템을 개발 할 것 이다.

