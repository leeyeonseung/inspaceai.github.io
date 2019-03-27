---
layout: post
title: "Keras 기반 F-RCNN 실습"
author: "정한솔"
date: 2017-09-19 14:00:00
categories: [Tutorials, Object Detection]
tags: [Object Detection, FRCNN]
---

본 포스트에서는 [Keras 기반으로 구현한 Faster RCNN](https://github.com/inspace4u/keras-frcnn) 코드를 직접 실행 및 실습해 보겠습니다.

---

### 실행 환경

이 예제에서는 기본적인 Tensorflow와 Keras 이외에 이미지 처리를 위한 [OpenCV](http://opencv.org/) 라이브러리와 대용량 데이터를 다루는 포맷인 hdf5를 지원하기 위한 [h5py](http://www.h5py.org/) 패키지가 추가로 필요합니다. 만약 [Windows 10에서 텐서플로우, 케라스 오프라인 설치]({{ "/lecture/2017/10/13/Windows_10_Keras_Offline_Install.html" | prepend: site.baseurl }}) 또는 [Windows 7]({{ "/lecture/2017/10/13/Windows_7_Keras_Offline_Install.html" | prepend: site.baseurl }}) 포스트의 설명을 따라 환경을 구축하셨다면 이 두 패키지가 이미 환경에 포함되어 있으니 신경 쓰지 않으셔도 됩니다.

```
pip install opencv-python h5py
```

만약 저 패키지가 설치되어 있지 않은 경우, 위 명령어를 이용하여 해당 패키지를 설치할 수 있습니다. 이 설치 과정에서는 온라인 연결이 필요합니다.

```
pip download opencv-python h5py
```

완전한 오프라인 설치가 필요한 경우 온라인 연결이 가능한 환경에서 위 명령어를 통해 다운로드 받은 .whl 파일들을 오프라인 환경으로 이동시킨 다음에,

```
pip install --no-index --find-links=. opencv-python h5py
```

저번 포스트의 오프라인 설치 방법과 같이 위 명령어를 통해 설치할 수 있습니다. (두 환경 사이에 OS 버전 및 Python 버전이 같지 않은 경우 설치가 실패할 수 있으니 주의하시기 바랍니다)

두 라이브러리를 설치 완료하였으면 실습을 위한 코드를 다운로드 받습니다. [Git](https://git-scm.com/)를 사용할 수 있는 온라인 환경이라면 다음 명령어를 통해 소스 코드를 다운로드 할 수 있습니다.

```
C:\Users\user> cd "C:\Projects\anaconda\_keras"
C:\Projects\anaconda\_keras> git clone https://github.com/inspace4u/keras-frcnn.git
```

C:\Projects\anaconda\_keras\keras-frcnn 폴더 아래에 소스가 위치하게 됩니다. Git가 없거나 오프라인 환경인 경우 Zip 압축 파일을 [이 링크](https://github.com/inspace4u/keras-frcnn/archive/master.zip)에서 다운로드 받을 수 있습니다. C:\Projects\anaconda\_keras 폴더 아래에 압축을 풉니다.

---

### 모델 훈련 및 예측

모델 훈련은 train_frcnn.py를 사용합니다. 먼저 훈련용 데이터셋이 필요합니다. [Keras 기반 F-RCNN의 원리]({{ "/lecture/2017/09/06/Keras_FRCNN_Description.html" | prepend: site.baseurl }}) 포스트를 참조하여 데이터셋을 구성해야 합니다. 직접 구성하거나 미리 구성된 데이터셋을 가져올 수 있습니다. 여기선 [PASCAL VOC 2012 홈페이지](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/index.html)에서 다운로드 받을 수 있는 [데이터셋](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar)을 사용하겠습니다. 해당 tar 파일(1.9GB)을 다운받아 keras-frcnn 폴더에 압축을 풉니다. (keras-frcnn 폴더 바로 아래에 VOCdevkit 폴더가 위치하도록 압축을 해제하시기 바랍니다) 그리고 아나콘다 콘솔창에 다음 명령어를 입력합니다.

```
C:\Projects\anaconda\_keras> cd keras-frcnn
C:\Projects\anaconda\_keras\keras-frcnn> python train_frcnn.py --path VOCdevkit
```

환경에 따라 훈련 소요 시간이 무척 오래 걸릴 수 있습니다. 필자의 엔비디아 Titan Xp GPU를 사용하는 환경에서 훈련 1회당 약 10분의 시간이 소요되었습니다. 2000회 훈련된 모델 파일을 아래에서 다운로드 받으실 수 있습니다.

* [frcnn_weight.zip](https://1drv.ms/u/s!AtbRowIzP4wEhO8W0aY9tOIRq3UtWA) (100MB)

예측은 test_frcnn.py를 사용합니다. keras-frcnn 폴더 아래에 images 폴더와 result_imgs 폴더를 생성합니다.

```
C:\Projects\anaconda\_keras\keras-frcnn> mkdir images
C:\Projects\anaconda\_keras\keras-frcnn> mkdir result_imgs
```

그리고 생성한 images 폴더 아래에 객체 검출할 예제 이미지를 넣습니다. 예측에 사용할 이미지는 인터넷에서 다운로드 받거나 직접 찍은 사진, 즉 훈련용 데이터셋에 포함되지 않는 이미지를 사용하는게 바람직합니다. 그리고 다음 명령어를 입력해 예측 스크립트를 실행합니다.

```
C:\Projects\anaconda\_keras\keras-frcnn> python test_frcnn.py --path images
```

result_imgs 폴더에 결과 파일이 출력되는 것을 볼 수 있습니다.

![result of frcnn prediction #1]({{ "/images/hansoli/result1.png" | prepend: site.baseurl }})
![result of frcnn prediction #2]({{ "/images/hansoli/result2.png" | prepend: site.baseurl }})
![result of frcnn prediction #3]({{ "/images/hansoli/result3.png" | prepend: site.baseurl }})
