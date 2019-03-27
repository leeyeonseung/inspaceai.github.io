---
layout: post
title: "[Unsupervised Anomaly Detection with GANs to Guide Marker Discovery] Paper Review"
author: "박상민"
date: 2019-03-25 12:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection, GAN]
---

본 포스트는 Spacecraft Telemetry 데이터의 특징 분석과 Anomaly Score 모델을 적용한 논문을 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.


# 2. Unsupervised Anomaly Detection with GANs to Guide Marker Discovery

* 망막 이미지 데이터의 이상징후를 감지하고, 마커로 표시하기위해 비지도학습 모델을 제안

* 정상 데이터만을 이용하여 학습시킨 GAN 모델을 사용해 query 이미지의 정상/비정상 여부와 비정상 영역을 찾아내고자 함  
  
   ![Paper_13]({{ "/images/sangmin/paper_13_1.png" | prepend: site.baseurl }})


### __Method__

* 정상 이미지 데이터에서 임의의 위치에서 랜덤하게 c x c 크기의 패치이미지 추출

* 정상 데이터를 이용하여 GAN 학습 

* Generative 모델은 fake 이미지를 real 이미지와 유사하게 만들기위해 real 이미지의 latent space를 맵핑  
   
    ![Paper_13]({{ "/images/sangmin/paper_12_2.png" | prepend: site.baseurl }})

* G모델이 만든 fake 이미지와 real image를 구별하도록(판별) Discriminator를 훈련

* 훈련된 Generator & Discriminator의 파라미터를 고정한 채 Queary 이미지를 G모델에 입력

* 정상 이미지의 경우 학습된 정상 이미지의 latent space(z)로 맵핑이 되지만, 비정상 이미지일 경우 벗어나게 됨 -> cost function의 오차가 발생  
  
    ![Paper_13]({{ "/images/sangmin/paper_12_3.png" | prepend: site.baseurl }})


* Anomaly Score가 높으면 비정상 이미지 / 낮으면 정상 이미지
  
    ![Paper_13]({{ "/images/sangmin/paper_12_4.png" | prepend: site.baseurl }})


### Dataset

* 망막층을 관측하는 빛간섭단층촬영(OCT) 영상을 사용

* 학습 데이터 셋
   * 정상 OCT 2D 이미지 패치
   * 64x64 사이즈의 추출한 1,000,000(100만) 2D 이미지
   * 정규화(-1 ~ 1) 

* 테스트 데이터 셋
   * 10개의 정상 데이터 셋과 10개의 비정상 데이터 셋 이용
   * 8,192개의 이미지 패치를 이용

### Model Architecture

* DCGAN 구조 사용하여 64x64 사이즈의 이미지를 학습   
  
    ![Paper_13]({{ "/images/sangmin/paper_13_5.png" | prepend: site.baseurl }})


* 채널 (1024-512-256-128) -> 채널 (512-256-128)

### Results

* 모델 결과

    ![Paper_13]({{ "/images/sangmin/paper_13_6.png" | prepend: site.baseurl }})

* 타 모델과의 성능지표 비교  
  
    ![Paper_13]({{ "/images/sangmin/paper_12_7.png" | prepend: site.baseurl }})

