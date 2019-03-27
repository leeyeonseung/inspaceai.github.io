---
layout: post
title: "[Satellite Image Forgery Detection and Localization Using GAN and One-Class Classifier] Paper Review"
author: "박상민"
date: 2019-03-25 12:00:00
categories: [Review, Anomaly Detection]
tags: [Anomaly Detection, AutoEncoder, SVM]
---

본 포스트는 Spacecraft Telemetry 데이터의 특징 분석과 Anomaly Score 모델을 적용한 논문을 간단하게 정리한 글 입니다.

---

> 작성자 : 박상민 - (주)인스페이스 미래기술실 연구원 
>
> 본 포스트는 약 4개월간 이상감지(Anomaly Detection)를 연구하게 되면서 공부했던 논문, 구현체 등을 정리해 공유하는 글 입니다. 
>
> 항공우주분야의 이상감지를 연구해왔기 때문에 대부분의 내용이 도메인에 밀접한 내용이 있으니 참고하시면 좋을 것 같습니다.


# 12. Satellite Image Forgery Detection and Localization Using GAN and One-Class Classifier[12](https://arxiv.org/pdf/1802.04881.pdf)

* 위성 영상 위조 검출 및 위치 인식을 위해 딥러닝 기반의 알고리즘 

* 위조 이미지는 이상(anomaly)으로 판별  

* 학습된(정상)이미지 외에 이상 객체가 발견될 경우 mask로 영역표시
  
  ![Paper_12]({{ "/images/sangmin/paper_12_1.PNG" | prepend: site.baseurl }})

## Model Architecture

* Autoencoder를 이용하여 iamge로부터 feature(h)를 구하고, 이를 다시 복원
* 복원된 이미지와 원 이미지를 이용하여 GAN을 훈련 -> Autoencder보다 약간의 성능향상
* 정상 이미지에 대한 latent space의 distribution을 찾아냄  

    ![Paper_12]({{ "/images/sangmin/paper_12_2.PNG" | prepend: site.baseurl }})

* 4개의 autoencoder 구조  

    ![Paper_12]({{ "/images/sangmin/paper_12_6.PNG" | prepend: site.baseurl }})

  
## Method

1. 오토인코더와 SVM은 정상(pristine) 이미지만을 이용해 학습

2. 이미지는 64×64 픽셀 크기의 패치로 분할

3. 학습된 오토인코더는 패치를 더 낮은 차원의 벡터(h)로 인코딩

4. h를 입력으로 받은 One-Class SVM은 정상 패치에서 학습한 feature 분포와 관련하여 위조 된 패치를 이상징후로 탐지하는 데 사용됨

5. 모든 패치가 분류되면 모든 패치 레이블을 그룹화하여 전체 이미지에 대한 레이블 마스크를 얻음
  
    ![Paper_12]({{ "/images/sangmin/paper_12_4.PNG" | prepend: site.baseurl }})

## Dataset

* 650 X 650 사이즈 130개의 이미지

* 30개는 학습과 검증에 사용, 남은 100개는 테스트에 사용

* 검출대상물의 크기에 따라 성능평가  
   * Small - Object size is smaller than the patch size (approximately 32 pixel per side)
   * Medium - Object size is comparable to patch size (approximately 64 pixel per side)
   * Large - Object size is larger than patch size (approximately
   128 pixel per side)  
     
    ![Paper_12]({{ "/images/sangmin/paper_12_5.PNG" | prepend: site.baseurl }})

## Result

* Detection Result AUC 
  
    ![Paper_12]({{ "/images/sangmin/paper_12_7.PNG" | prepend: site.baseurl }})


    ![Paper_12]({{ "/images/sangmin/paper_12_9.PNG" | prepend: site.baseurl }})

* Localization Result AUC 
  
    ![Paper_12]({{ "/images/sangmin/paper_12_8.PNG" | prepend: site.baseurl }})

    ![Paper_12]({{ "/images/sangmin/paper_12_10.PNG" | prepend: site.baseurl }})
