---
layout: post
title: "객체 검출을 위한 가이드"
author: "정한솔"
date: 2019-03-26 16:00:00
categories: [Tutorials, Object Detection]
tags: [Object Detection]
---

이 포스트는 현재 작성중. (작성 끝나면 제목 바꿀 예정이니 수정하지 말 것) by 정한솔

---

본 포스트에서는 [처음부터 끝까지: 딥 러닝을 사용한 객체 검출을 위한 가이드: Faster R-CNN, YOLO, SSD](https://cv-tricks.com/object-detection/faster-r-cnn-yolo-ssd/)를 한국어로 번역하여 소개하겠습니다. 딥 러닝 기반 객체 검출의 기초 개념 학습에 도움이 될 것으로 생각됩니다.

This article is a translation of [Zero to Hero: Guide to Object Detection using Deep Learning: Faster R-CNN, YOLO, SSD](https://cv-tricks.com/object-detection/faster-r-cnn-yolo-ssd/).

---

이 포스트에서는 객체 검출과 Faster R-CNN, YOLO, SSD와 같은 다양한 알고리즘을 소개할 예정입니다. 초보자 수준부터 시작하여 객체 검출에 있어서의 최첨단 알고리즘까지 넓게 다룰 것이며, 각 알고리즘의 핵심적인 요소 및 접근 방법에 대해서 이해합니다.

## 이미지 분류란?

이미지 분류 문제는 이미지를 받아 그 이미지 안에 어떤 객체가 존재하는지 예측합니다. 예를 들어 고양이와 개를 분류하는 분류 모델을 만들었다면 다음과 같이 고양이나 개 이미지를 받아 그 분류를 추측할 수 있습니다.

![](https://cv-tricks.com/wp-content/uploads/2017/12/classification-cat-vs-dog-300x195.jpg)

하지만 만약 이미지 안에 고양이와 개가 동시에 존재한다면 어떻게 분류해야 될까요?

![](https://cv-tricks.com/wp-content/uploads/2017/12/cat_dog-300x200.jpeg)

이 문제를 해결하기 위해서는 두 분류를 동시에 검출할 수 있는 다중 분류 모델을 사용해야 합니다. 하지만 그렇게 하더라도 이미지의 어느 부분이 고양이고 어느 부분이 개를 나타내는지에 관한 정보는 얻을 수 없습니다. 이미지 내에서 (분류가 알려져 있는) 특정 객체의 위치가 어디인지 판별하는 문제는 **지역화**라고 부릅니다. 하지만 분류가 미리 주어져 있지 않은 경우 지역화를 위해서는 객체의 분류를 함께 구할 필요가 있습니다.

![](https://cv-tricks.com/wp-content/uploads/2017/12/detection-vs-classification-300x220.png)

객체의 분류와 위치를 같이 예측하는 문제는 **객체 검출**이라고 부릅니다. 이미지에서 객체의 분류만을 예측하는 대신에 객체를 포함하는 범위의 사각형을 함께 추측해야 합니다. (이 사각형을 경계 상자라고 부릅니다) 따라서 이미지 안의 객체 하나마다 다음과 같은 값을 구해야 합니다.

* 분류 이름
* 경계 상자의 좌상단 x 좌표
* 경계 상자의 좌상단 y 좌표
* 경계 상자 너비
* 경계 상자 높이

한 이미지 안에 여러 종류의 객체가 존재하는 경우 다중 분류 모델과 유사하게 여러 종류의 객체를 동시에 검출할 수 있는 모델을 사용하여야 합니다.

![](https://cv-tricks.com/wp-content/uploads/2017/12/Multi-class-object-detection.png)

이제부터 객체 검출기를 훈련하기 위해 자주 쓰이는 방법론에 대해서 소개하겠습니다. 역사적으로 객체 검출을 위한 알고리즘은 2001년에 Viola, Jones 등이 제안한 Haar Cascades 분류기 이래 다양한 방법이 제안되었지만 여기에서는 신경망과 딥 러닝을 이용하는 첨단 알고리즘에 주목하겠습니다.

객체 검출은 가능한 모든 위치에서 정해진 사이즈의 윈
