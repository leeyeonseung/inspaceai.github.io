---
layout: post
title: "Introduction to XAI"
author: "이현호"
date: 2019-03-20 14:00:00
categories: [Tutorials, XAI]
tags: [XAI]
---

본 포스트에서는 eXplainable AI(XAI)에 대해 간략히 알아보겠습니다.
본 포스트의 자료는 대부분 [Interpretable-ml-book](https://christophm.github.io/interpretable-ml-book/) 에서 참조하였습니다.

![Interpretable-ml-book]({{ "/images/lhh/interpretable-ml-book.png" | prepend: site.baseurl }})

---

## XAI

인공지능분야가 빠른 속도로 발전하면서 일상생활의 많은 문제들에 인공지능을 많이 적용하려는 시도를 볼 수 있습니다. 대부분의 인공지능 모델은 Black Box 모델로 특성상 출력값에 대한 설명을 따로 해주지 않습니다. 인공지능 모델의 출력값이 큰 영향을 미치지 않는 사소한 문제에만 적용한다면 사실 XAI는 중요하지 않을 수 있습니다. 하지만 인공지능 모델의 출력값이 큰 영향을 미치는 예를 들어 자율주행문제에 AI를 적용한다면 얘기는 달라집니다. 인공지능 모델이 출력한 값의 원인을 판단하여 모델이 올바르게 작동되고 있는지를 판단하는 것은 중요한 문제입니다. 이런 문제를 해결하기 위해 인공지능 모델을 설명해줄수 있는  XAI가 필요합니다.

XAI란 eXplainable Artificial Intelligence의 줄임말로 설명가능한 인공지능을 의미합니다. 이는 Interpretable AI, 해석가능한 인공지능이라고도 합니다. 

## Interpretability

[Interpretable-ml-book](https://christophm.github.io/interpretable-ml-book/) 에서는 Interpretability의 정의를 다음과 같이 설명합니다.

- 사람이 AI 모델의 출력값의 원인을 이해할 수 있는 정도
- 사람이 AI 모델의 출력값을 예측할 수 있는 정도

위 정의들을 보았을 때 Interpretability란 사람이 모델을 얼마나 이해하고 있는지에 대한 척도로 생각할 수 있습니다.

## Interprebability Methods

AI 모델을 해석하기 위해 크게 두 가지 방법이 있습니다.

 - ## Interpretable Model
    모델을 해석하기 위한 첫 번째 방법은 Interpretable Model을 사용하는 것입니다. Interpretable Model은 대체적으로 내부구조가 간단하게 구성되어 있습니다. 모델이 간단하면 보다 쉽게 내부(ex. weight)를 해석을 할 수 있기 때문입니다. Interpretable Model로 다음과 같은 것들이 있습니다.

    - Linear Regression
    - Logistic Regression
    - GLM
    - GAM
    - Decision Tree
    - Decision Rules
    - RuleFit, Naive Bayes Classifier
    - K-Nearst Neighbors
    
 - ## Model-Agnostic Method
    모델을 해석하기 위한 두 번째 방법은 Model-Agnostic Method가 있습니다. 이는 Interpretable Model과 다르게 어떠한 AI 모델에 적용할 수 있습니다. 즉, 학습된 모델을 가지고 실험하면서 모델을 이해하는 방식 입니다. Model-Agnostic Method로 다음과 같은 것들이 있습니다.

     - Partial Dependence Plot
     - Individual Conditional Expectation
     - Acculated Local Effects
     - Feature Interaction
     - Feature Importance
     - Global Surrogate
     - Local Surrogate
     - Shapley Values
