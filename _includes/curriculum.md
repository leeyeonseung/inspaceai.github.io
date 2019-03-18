## 딥러닝 기초

* 개발 환경 구축
    * Python
    * Deep Learning
* 파이썬 기초
    * Python 기초
    * Numpy
    * Matplotlib
    * pandas
* 신경망
    * 활성화 함수(Activation Function)
        * 시그모이드
        * 계단 함수
        * ReLU
    * 은닉층
    * 출력층
* 손실 함수(Loss Function)
    * MSE
    * Cross Entropy Error
* 오차역전파
    * 원리 이해
    * 구현
* Optimizer
    * SGD
    * Momentum
    * Adagrad
    * Adam
* 모델 학습
    * Batch size
    * epoch
    * Learning rate
    * Overfitting
    * Dropout
* 모델 평가
    * [Intersecton over Union]({{ "/2017/09/28/IoU" | prepend: site.baseurl }})
    * [Mean Average Precision]({{ "/2017/11/07/Mean_Average_Precision" | prepend: site.baseurl }})
* 데이터 셋 이야기
    * 훈련 셋
    * 검증 셋
    * 시험 셋
* Linear Regression
    * 가설함수
    * 비용 함수
    * 구현
* Logistic Regression
    * 가설함수
    * 비용 함수
    * 구현
* Softmax Regression
    * 가설함수
    * 비용 함수
    * 구현
* CNN
    * 구조
    * 구현(Tensorflow, Keras)
    * AlexNet 등
* RNN & LSTM
    * RNN
    * LSTM

## 딥러닝 응용

* 분류
    * Google Net
    * AlexNet
    * ResNet
    * VGG
* Object Detection
    * Faster R-CNN [이론]({{ "/2017/09/06/Keras_FRCNN_Description" | prepend: site.baseurl }})/[실습]({{ "/2017/09/19/Keras_FRCNN_Testing" | prepend: site.baseurl }})
        * [Non Max Suppression]({{ "/2017/09/27/NMS_Algorithm" | prepend: site.baseurl }})
        * [Selective Search]({{ "/2017/09/29/Selective_Search" | prepend: site.baseurl }})
    * RetinaNet [이론]({{ "/2019/03/14/RetinaNet_Description" | prepend: site.baseurl }})
    * YOLO
    * SSD
* Semantic Segmentation
    * FCN
    * DeepLab v1, v2, v3
* Anomaly Detection
    * Time Series Decomposition
        * ARMA Model
        * Autoregressive model
        * Moving-averge model
    * clustering
    * Autoencoder
    * LSTM
    * VAE
    * GAN
* Fire Detection
    * FireNet
    * InceptionV1-OnFireNet
 * Generative Model
    * VAE
    * GAN
    * DCGAN
    * WGAN
    * CGAN
    * Cycle GAN
 * image to image translation
    * Pix2Pix
    * Cycle GAN
* XAI
    * Interpretable Models
        * Linear Regression
        * Logistic Regression
        * GLM, GAM
        * Decision Tree
    * Model-Agnostic Methods
        * PDP
        * ICE
        * ALE
* Decomposition of Time Series
    * ARMA Model
        * Autoregressive
        * Moving-averge
* Data Analysis
    * PCA
    * t-SNE
    * Clustering
* Graph Neural Network
    * Graph Convolutional Networks
    * Graph Attention Networks
    * Gated Graph Neural Networks
    * Graph LSTM
* Embedded AI
* Natural Language Processing
    * RNN
    * LSTM
    * GRU
    * Word2Vec
* Domain Adaptaion
* Meta Learning
* Uncertainty in Deep Learning
* Efficient Inference Methods
* Efficient Training Methods

## 강화학습

* Model-Based RL
* Multi-Agent RL
* Navigation
* Hierarchical RL
* Markov Decision Processes
* DQN
* Unity ML Agent
