https://github.com/lexfridman/mit-deep-learning
# MIT-Deep Learnig Review

# 목차

[1. 딥러닝 기초](#Deep-Learning-Basics)            
[1.1 전제 조건](#Prerequisites)             
[1.2 Feed-Forward 신경망에 의한 Bostan 주택가격 예측](#Boston-Housing-Price-Prediction-with-Feed-Forward-Neural-Networks)         
<bar> [1.2.1 모델 설정](#Build-the-model)                
<bar> [1.2.2 모델 학습](#Train-the-model)                    
[1.3 합성신경망을 이용한 MNIST 꿈의 분류](#Classification-of-MNIST-Dreams-with-Convolutional-Neural-Networks)                 
<bar> [1.3.1 모델 설정](#Build-the-model)               
<bar> [1.3.2 모델 학습](#Train-the-model)                
<bar> [1.3.3 정확도 평가](#Evaluate-accuracy)                   
<bar> [1.3.4 예측](#Make-predictions)                  

[2. 운전 장면 분할](#Driving-Scene-Segmentation)            
[GAN (Generative Adversarial Network)](#Generative-Adversarial-Networks)          
[DeepTraffic 심층 강화 학습 대회](#DeepTraffic-Deep-Reinforcement-Learning-Competition)          

# Deep Learning Basics

이 문서는 MIT Deep Learning의 일부로 제공되는 [기초 강의](https://www.youtube.com/watch?list=PLrAXtmErZgOeiKm4sgNOknGvNjby9efdf&v=O5xeyoRL95U)를 바탕으로 만들어졌다. 이 문서에서는 Deep Learning에서 7가지 중요한 유형/개념/접근법에 대해 언급한다. 이 7가지는 아래 그림과 같이 표현된다.

![1](https://camo.githubusercontent.com/aa717ae5a4ce2302a6ba50c1c1a532fd566dd236/68747470733a2f2f692e696d6775722e636f6d2f45416c343772702e706e67)

높은 수준의 신경망은 각각의 인코더, 디코더 또는 두 가지 모두의 조합이다. **인코더**는 원시 데이터에서 패턴을 찾아 적고 유용한 표현을 생성한다. **디코더**는 이러한 표현에서 새로운 데이터 또는 고해상도 유용한 정보를 생성한다. 강의에서 설명한 것처럼 Deep Learning은 세상을 **표현하는 방법**을 발견하여 우리가 그것에 대해 추론할 수 있게 한다. 나머지는 시각 정보, 언어, 소리(1~6)를 효과적으로 사용하고, 가끔 제공되는 보상을 기반으로 하는 세계에서 활동할 수 있도록 도와주는 현명한 방법도 존재한다(7).

> **1. Feed Forward Neural Networks (FFNNs)**       
  형상에 따른 분류 및 회귀 분석([1.2 참조](#Boston-Housing-Price-Prediction-with-Feed-Forward-Neural-Networks))           
  **2. Convolutional Neural Networks (CNNs)**         
  이미지 분류, 객체 감지, 비디오 행동 인식 등([1.3 참조](#Classification-of-MNIST-Dreams-with-Convolutional-Neural-Networks))         
  **3. Recurrent Neural Networks (RNNs)**         
  언어 모델링. 음성 인식 등([TF 튜토리얼 참조](https://www.tensorflow.org/tutorials/text/text_generation))         
  **4. Encoder Decoder Architectures**           
  의미 분할, 기계 번역 등([2 참조](#Driving-Scene-Segmentation))
  **5. Autoencoder**
  비지도 파견, 노이즈 제거 등
  **6. Generative Adversarial Networks (GANs)**
  현실적 이미지의 비지도적 생성 등
  **7. Deep Reinforcement Learning**
  게임 플레이, 시뮬레이션의 로봇 공학, 신경 구조 검색 등
  
이러한 튜토리얼에는 기본 아이디어의 핵십을 잃지 않고 선별적인 손실과 단순화가 존재한다. 아래의 아인슈타인 인용구를 보아라  

![2](https://camo.githubusercontent.com/c3db3435e3a1ed35c4061b831954bf0fe42969d6/68747470733a2f2f692e696d6775722e636f6d2f7666504448474e2e706e67)

## Prerequisites

tf.keras는 TensorFlow에서 신경망 모델을 구축하고 훈련하는 가장 간단한 방법이다. 따라서, 이 문서에서는 모델이 하위 레벨의 API를 사용하지 않고 이 방법을 사용할 것이다. 

tf.keras(TensorFlow와 함께 제공됨)와 Keras(독립형)가 있다. tf.kears는 TensorFlow와 함께 제공되므로 추가 설치가 필요하지 않고, 강력한 TensorFlow 고유 기능이 제공되므로 이것을 사용할 것이다. 

```python
# TensorFlow와 tf.keras
import tensorflow as tf
from tensorflow import keras
from tensorflow.keras.layers import Conv2D, MaxPooling2D, Dropout, Flatten, Dense

# 일반적으로 사용되는 모듈
import numpy as np
import os
import sys

# 이미지, 그림, 표시, 시각화
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
import cv2
import IPython
from six.moves import urllib
```

## Boston Housing Price Prediction with Feed-Forward Neural Networks

### Build the model

### Train the model

## Classification of MNIST Dreams with Convolutional Neural Networks

### Build the model

### Train the model

### Evaluate accuracy

### Make predictions












# Driving Scene Segmentation

# Generative Adversarial Networks

# DeepTraffic Deep Reinforcement Learning Competition
