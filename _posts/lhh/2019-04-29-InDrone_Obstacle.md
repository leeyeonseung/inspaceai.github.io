---
layout: post
title: "InDrone 환경 이용하여 드론 장애물 환경 제작"
author: "이현호"
date: 2019-04-30 18:00:00
categories: [Projects, Unity ML-Agents]
tags: [Reinforcement Learning, Unity ML-Agents, Drone]
---

본 포스트에서는 (주)인스페이스에서 제작한 유니티 기반 드론 강화학습 환경을 이용하여 드론 장애물 환경을 제작해보도록하겠습니다.
  
저장소 링크 : [https://github.com/InSpaceAI/RL-InDrone](https://github.com/InSpaceAI/RL-InDrone)

<img src="{{"/images/lhh/do/19.gif" | prepend: site.baseurl }}" style="max-width:100%" alt="Finish">

---
지금부터 기존 환경을 이용하여 위 환경을 제작해보겠습니다.

먼저 저장소 링크에 있는 UnitySDK를 유니티로 열고 Project창에 있는 DroneFlight 환경을 클릭하고 Ctrl+D를 눌러 복제합니다.

<img src="{{"/images/lhh/do/1.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Duplicate">

복제를 하면 다음과 같은 폴더가 생성 됩니다.

<img src="{{"/images/lhh/do/2.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Duplicated">

그럼 생성된 폴더에서 Drone Flight는 모두 Drone Obstacle로, DF는 모두 DO로 바꿔주겠습니다.

<img src="{{"/images/lhh/do/3.png" | prepend: site.baseurl }}" style="max-width:100%" alt="F->O">

다음 그림과 같이 Academy와 Agent 스크립트 안에있는 클래스도 바꿔줍니다.

<img src="{{"/images/lhh/do/4.png" | prepend: site.baseurl }}" style="max-width:100%" alt="DOAcademy">
<img src="{{"/images/lhh/do/5.png" | prepend: site.baseurl }}" style="max-width:100%" alt="DOAgent">

다음으로 장애물을 생성해보겠습니다.

먼저 DOGame을 우클릭하여 3DObject -> Shpere 클릭하여 Sphere를 생성하고 아래 그림과 같이 Inspector를 변경해줍니다. Collider를 제거하여 드론이 장애물을 통과할 수 있게 해줍니다(드론과 장애물이 일정거리 이상 가까워지면 실패처리를 하기 위함)

<img src="{{"/images/lhh/do/6.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Obstacle">

그 다음으로 Project 창의 Materials을 우클릭하고 Create-> Material을 통해 Obstacle Material을 생성해주고 Hierachy의 Obstacle에 드래그하여 임포트하고 Obstacle Material을 클릭하여 Inspector의 Albedo 옆의 색을 클릭하여 Color창을 띄우고 원하는 색으로 변경합니다.

<img src="{{"/images/lhh/do/7.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Color Change">

현재까지 작업을 잘 마쳤으면 다음 그림과 같은 상황이 됩니다.

<img src="{{"/images/lhh/do/8.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Current Status">

현재까지 잘 진행이 되었다면 이제 DOAgent 스크립트를 수정해보겠습니다.

먼저 장애물을 추가하기 위해 아래 그림과 같이 다음 코드를 추가해줍니다.

```C#
public GameObject obstacle; 
```

<img src="{{"/images/lhh/do/9.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Add Obstacle Code1">

그리고 에이전트에게 장애물 위치를 상태로 알려주기 위해 CollectObservations 함수에 아래 그림과 같이 다음 코드를 추가해줍니다.

```C#
AddVectorObs(obstacle.transform.position - gameObject.transform.position);
```

<img src="{{"/images/lhh/do/10.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Add Obstacle Code2">

그 다음 장애물에 일정거리에 도달하면 실패하도록 하기 위해 AgentAction 함수의 실패 조건이 있는 부분에 아래 그림과 같이 다음 코드를 추가해줍니다.

```C#
obstacle.transform.position - gameObject.transform.position).magnitude<0.3f
```

<img src="{{"/images/lhh/do/11.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Add Obstacle Code3">


그 다음 에피소드가 리셋이 되었을때 목적지 및 드론 장애물을 설정하기 위해 아래 그림과 같이 AgentReset()에 목적지 생성 부분을 수정하고 장애물 생성 코드를 추가합니다.

```C#
var theta1 = Random.Range(-Mathf.PI, Mathf.PI);
var theta2 = Random.Range(-Mathf.PI, Mathf.PI);
var radius = Random.Range(1f, 5f);

goal.transform.position = droneInitPos + 
                        new Vector3(radius * Mathf.Sin(theta1) * Mathf.Cos(theta2),
                        radius * Mathf.Sin(theta1) * Mathf.Sin(theta2),
                        radius * Mathf.Cos(theta1));

obstacle.transform.position = droneInitPos +
                        (goal.transform.position - droneInitPos) * Random.Range(0.3f, 0.8f) +
                        new Vector3(Random.Range(-0.2f, 0.2f),
                                    Random.Range(-0.2f, 0.2f),
                                    Random.Range(-0.2f, 0.2f)); //Noise term
```

<img src="{{"/images/lhh/do/12.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Add Obstacle Code4">

먼저 좌표계를 사용하지 않고 극좌표계를 사용한 이유는 드론과 목적지 사이의 거리를 조절하기 쉽게 하기 위함입니다. 장애물이 어느정도 목적지까지 가는 경로에 생성되기를 원했고, 만약 이 경우 드론과 목적지가 너무 가까워지면 장애물 또한 드론에 가까워져 에피소드가 시작과 동시에 실패하게됩니다. 이 경우를 막기 위해 드론과 목적지 사이의 거리를 조절하게 되었습니다. 따라서 이를 통해 목적지를 드론에서부터 1~5 사이에 생성시켰고 장애물을 이 사이에 랜덤한 비율에 노이즈를 추가하여 생성하였습니다.

이렇게 Agent 스크립트 수정을 마쳤습니다.

다음으로 이 전에 드론과 장애물 사이의 벡터를 Observation으로 추가한 것을 적용하기 위해 Brain의 Vector Observation 차원을 아래 그림과 같이 15에서 18로 변경해줍니다.

<img src="{{"/images/lhh/do/13.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Observation dimension change">

그리고 DOAcademy, Drone에 DFAcademy, DFAgent 스크립트를 제거하고 DOAcademy, DOAGents를 추가합니다. 그리고 아래 그림과 같이 DOAcademy에 DOLearningBrain을 넣어주고 Control을 체크, DOAgent에 해당 설정변수들을 넣어줍니다.

<img src="{{"/images/lhh/do/14.png" | prepend: site.baseurl }}" style="max-width:100%" alt="DOAcademy">
<img src="{{"/images/lhh/do/15.png" | prepend: site.baseurl }}" style="max-width:100%" alt="DOAgent">

자 그럼 이제 환경 제작을 마쳤으니 ml-agents 내장 ppo를 통해 학습해보도록 하겠습니다.

빌드할 때 아래 그림처럼 환경을 여러개로 복제하여 학습을 진행하면 보다 안전하고 빠르게 학습을 할 수 있습니다.

<img src="{{"/images/lhh/do/16.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Multi Agents">

그러면 내장 ppo를 통해 학습을 진행합니다. 내장 ppo 학습 관련 자세한 사항에 대해서는 [튜토리얼](https://github.com/hyunho1027/Unity_ML_Agents_Tutorial)을 참고하세요

<img src="{{"/images/lhh/do/17.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Learning">

학습이 완료되었다면 모델이 저장된 경로에 들어가 DroneObstacle의 TFModels 폴더에 복사해줍니다.

<img src="{{"/images/lhh/do/18.png" | prepend: site.baseurl }}" style="max-width:100%" alt="Model">

그리고 새로 복사한 모델을 적용하고 플레이하여 잘 작동되는지 확인합니다.

<img src="{{"/images/lhh/do/19.gif" | prepend: site.baseurl }}" style="max-width:100%" alt="Finish">

이상 여기까지 기존 환경을 이용해서 새로운 환경을 제작하는 포스트를 마치겠습니다.