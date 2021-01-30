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

![](https://camo.githubusercontent.com/aa717ae5a4ce2302a6ba50c1c1a532fd566dd236/68747470733a2f2f692e696d6775722e636f6d2f45416c343772702e706e67)

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

![](https://camo.githubusercontent.com/c3db3435e3a1ed35c4061b831954bf0fe42969d6/68747470733a2f2f692e696d6775722e636f6d2f7666504448474e2e706e67)

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

집값을 예측하기 위해 완전히 연결된 신경망을 사용하는 것부터 시작해보자. 다음 이미지에서는 회귀 분석과 분류 간의 차이를 강조한다(1.3 참조). 관측치를 입력으로 지정하면 회귀 분석에서는 연속 값(예: 정확한 온도)을 출력하고 분류에서는 관측치가 속한 클래스/범주를 출력한다. 

![](https://camo.githubusercontent.com/e77fa163f6a3ca8b73eecbc3562322a463999ab3/68747470733a2f2f692e696d6775722e636f6d2f7676536f417a672e6a7067)

Boston 집 데이터 세트의 경우 각각 13개의 기능이 있는 506개의 데이터 행이 있다. 우리의 과제는 이 13가지 기능을 입력 및 출력으로 사용하는 회귀 모델을 구축하여 "소유자 거주 주택의 중간 가치(1000달러 단위)"를 예측하는 것이다.

데이터 세트를 로드하면 다음과 같은 4개의 Numpy 배열이 반환된다.
> train_images 및 train_labels 배열은 모델이 학습하는 데 사용하는 데이터인 교육 세트이다.          
  모델은 테스트 세트, test_images 및 test_labels 배열을 통해 테스트된다.

```python
(train_features, train_labels), (test_features, test_labels) = keras.datasets.boston_housing.load_data()

# 정규화할 교육 집합에서 특징별 통계량(평균, 표준 편차) 가져오기
train_mean = np.mean(train_features, axis=0)
train_std = np.std(train_features, axis=0)
train_features = (train_features - train_mean) / train_std
```

### Build the model

신경망을 구축하려면 모델의 계층을 구성한 다음 모델을 컴파일해야 한다. 먼저 *keras.Sequential*을 사용하여 몇 개의 계층 쌓는다. 다음으로 모니터링할 손실 함수, 최적화 도구, 메트릭을 구성한다. 이러한 기능은 모델의 컴파칠 단계에서 추가된다.

> Loss function : 훈련 중에 모형이 얼마나 정확한지 측정한다. 최적화 도구를 사용하여 이를 최소화하려고 한다.
  Optimizer : 모델이 보는 데이터와 손실 함수를 기반으로 모델을 업데이트하는 방법
  Metrics : 교육 및 테스트 단계의 모니터링에 사용

20개의 뉴런으로 구성된 1개의 은닉 계층으로 네트워크를 구축하고 평균 제곱 오차(MSE)를 손실 함수로 사용해보자.

```python
def build_model():
    model = keras.Sequential([Dense(20, activation=tf.nn.relu, input_shape=[len(train_features[0])]),Dense(1)])

    model.compile(optimizer=tf.train.AdamOptimizer(), loss='mse',metrics=['mae', 'mse'])
    return model
```

### Train the model

신경망 모델을 훈련하려면 다음과 같은 단계가 필요하다
```markdown
1. 교육 데이터를 모델에 제공이 예에서는 train_features 및 train_labels 배열)
2. 모델은 특징과 레이블을 연결하는 방법을 배운다
3. 우리는 모델에게 테스트 세트(이 예에서는 test_features 배열)에 대해 예측하도록 요청하고, 예측이 test_labels 배열의 레이블과 일치하는지 검증한다.
```

학습이 시작되면 모델 교육 데이터로 적합한 model.fit을 호출한다.
```python
# 출력물을 덜 상세하게 만들지만 진행상황을 보여준다.
class PrintDot(keras.callbacks.Callback):
    def on_epoch_end(self, epoch, logs):
        if epoch % 100 == 0: print('')
        print('.', end='')

model = build_model()

early_stop = keras.callbacks.EarlyStopping(monitor='val_loss', patience=50)
history = model.fit(train_features, train_labels, epochs=1000, verbose=0, validation_split = 0.1, callbacks=[early_stop, PrintDot()])

hist = pd.DataFrame(history.history)
hist['epoch'] = history.epoch

# https://www.kaggle.com/c/boston-housing/leaderboard에서 Kaggle 리더보드와 비교할 수 있는 RMSE 측정 방법을 보여준다.
rmse_final = np.sqrt(float(hist['val_mean_squared_error'].tail(1)))
print()
print('Final Root Mean Square Error on validation set: {}'.format(round(rmse_final, 3))
```

이제 교육 및 검증 세트에 대한 손실 함수 측도를 표시해보자. 유효성 검사 세트는 과적합을 방지하는 데 사용된다([참고자료](https://www.tensorflow.org/tutorials/keras/overfit_and_underfit)). 그러나 우리의 네트워크가 작기 때문에 그래프에서 보여 주는 것처럼 눈에 띄게 데이터를 과대 적합시키지 않고 훈련에 수렴된다.

```python
def plot_history():
    plt.figure()
    plt.xlabel('Epoch')
    plt.ylabel('Mean Square Error [Thousand Dollars$^2$]')
    plt.plot(hist['epoch'], hist['mean_squared_error'], label='Train Error')
    plt.plot(hist['epoch'], hist['val_mean_squared_error'], label = 'Val Error')
    plt.legend()
    plt.ylim([0,50])

plot_history()
```
![1](https://github.com/junsu9637/Study/blob/main/Artificial%20Intelligence/Montreal%20AI%20101%20-%20Cheet%20Sheet/Deep%20Learning/MIT-Deep%20Learning%20Review/Image/1.png?raw=true)

다음으로, 테스트 데이터 세트에서 모델의 성능을 비교한다.

```python
test_features_norm = (test_features - train_mean) / train_std
mse, _, _ = model.evaluate(test_features_norm, test_labels)
rmse = np.sqrt(mse)
print('Root Mean Square Error on test set: {}'.format(round(rmse, 3)))
```

## Classification of MNIST Dreams with Convolutional Neural Networks

데이터 세트 외부의 고해상도 필기 숫자에서 분류기를 테스트하는 MNIST 데이터 세트에서 손으로 쓴 자릿수의 이미지를 분류하는 컨볼루션 신경망(CNN) 분류기를 구축해보자.

```python
# 공통 상수 설정
this_repo_url = 'https://github.com/lexfridman/mit-deep-learning/raw/master/'
this_tutorial_url = this_repo_url + 'tutorial_deep_learning_basics'
```

MNIST 데이터 세트에는 28x28픽셀 해상도에서 손으로 쓴 숫자의 흑백 이미지가 70,000개 포함되어 있다. 우리의 작업은 다음 이미지 중 하나를 입력으로 가져와서 이미지에 포함될 가능성이 가장 높은 숫자를 예측하는 것이다(이 예측에 대한 상대적 신뢰도).

![](https://camo.githubusercontent.com/24545a9ca1aa3b5d1036bd3deaed3ed7ec6cfdc4/68747470733a2f2f692e696d6775722e636f6d2f4954726d3978342e706e67)

이제 데이터 세트를 로드한다. 이는 28x28 NumPy 배열로 픽셀 값은 0에서 255사이 이미지로 배열은 0~9 사이의 정수 배열이다. 

```python
(train_images, train_labels), (test_images, test_labels) = keras.datasets.mnist.load_data()

# 단일 채널로 지정하도록 이미지 재구성
train_images = train_images.reshape(train_images.shape[0], 28, 28, 1)
test_images = test_images.reshape(test_images.shape[0], 28, 28, 1)
```

신경망 모델에 공급하기 전에 이 값을 0-1 범위로 확장하기 위해 255로 나눈다. 교육 세트와 테스트 세트를 동일한 방식으로 사전 처리하는 것이 중요하다. 

```python
def preprocess_images(imgs): # 단일 이미지와 다중 이미지 모두에 대해 작동해야 함
    sample_img = imgs if len(imgs.shape) == 2 else imgs[0]
    assert sample_img.shape in [(28, 28, 1), (28, 28)], sample_img.shape # 이미지가 28x28 및 단일 채널인지 확인(흑백)
    return imgs / 255.0

train_images = preprocess_images(train_images)
test_images = preprocess_images(test_images)
```

교육 세트의 처음 5개의 이미지를 표시하고 각 이미지 아래에 클래스 이름을 표시한다. 그리고 데이터가 올바른 형식인지, 네트워크를 구축하고 교육할 준비가 되었는지 확인한다. 

```python

plt.figure(figsize=(10,2))
for i in range(5):
    plt.subplot(1,5,i+1)
    plt.xticks([])
    plt.yticks([])
    plt.grid(False)
    plt.imshow(train_images[i].reshape(28, 28), cmap=plt.cm.binary)
    plt.xlabel(train_labels[i])
```
![](https://github.com/junsu9637/Study/blob/main/Artificial%20Intelligence/Montreal%20AI%20101%20-%20Cheet%20Sheet/Deep%20Learning/MIT-Deep%20Learning%20Review/Image/2.png?raw=true)

### Build the model

신경망을 구축하려면 모델의 계층을 구성한 다음 모델을 컴파일해야 한다. 대부분의 경우 이 값을 단순히 겹겹이 쌓는 것으로 줄일 수 있다. 

```python
model = keras.Sequential()
# 각 3x3 크기의 컨볼루션 필터 32개 사용
model.add(Conv2D(32, kernel_size=(3, 3), activation='relu', input_shape=(28, 28, 1)))
# 각각 3x3 크기의 컨볼루션 필터 64개 사용
model.add(Conv2D(64, (3, 3), activation='relu'))
# 풀링을 통해 최상의 기능 선택
model.add(MaxPooling2D(pool_size=(2, 2)))
# 수렴 개선을 위해 뉴런을 무작위로 켜고 끔
model.add(Dropout(0.25))
# 너무 많은 차원이 있기 때문에 단지 분류 출력만을 원함
model.add(Flatten())
# 모든 관련 데이터를 얻기 위해 완전히 연결됨
model.add(Dense(128, activation='relu'))
# 한번 더 드롭아웃
model.add(Dropout(0.5))
# 행렬을 출력 확률로 압착하기 위해 소프트맥스를 출력
model.add(Dense(10, activation='softmax'))
```

모델이 교육을 받을 준비가 되기 전에 몇 가지 설정이 더 필요하다. 이러한 기능은 모델의 컴파일 단계에서 추가된다.
> Loss function : 훈련 중에 모형이 얼마나 정확한지 측정한다. 최적화 도구를 사용하여 이를 최소화             
  Optimizer : 모델이 보는 데이터와 손실 함수를 기반으로 모델을 업데이트하는 방법               
  Metrics : 교육 및 테스트 단계를 모니터링하는 데 사용. "정확도"는 정확하게 분류된 이미지의 일부이다.         

```python
model.compile(optimizer=tf.train.AdamOptimizer(), loss='sparse_categorical_crossentropy',metrics=['accuracy'])
```

### Train the model

### Evaluate accuracy

### Make predictions












# Driving Scene Segmentation

# Generative Adversarial Networks

# DeepTraffic Deep Reinforcement Learning Competition
