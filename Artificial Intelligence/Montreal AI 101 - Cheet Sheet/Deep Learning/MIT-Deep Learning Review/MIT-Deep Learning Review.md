https://github.com/lexfridman/mit-deep-learning
# MIT-Deep Learnig Review

# 목차

[1. 딥러닝 기초](#deep-learning-basics)            
[1.1 전제 조건](#prerequisites)             
[1.2 Feed-Forward 신경망에 의한 Bostan 주택가격 예측](#boston-housing-price-prediction-with-feed-forward-neural-networks)         
<bar> [1.2.1 모델 설정](#build-the-model)                
<bar> [1.2.2 모델 학습](#train-the-model)                    
[1.3 합성신경망을 이용한 MNIST 꿈의 분류](#classification-of-mnist-dreams-with-convolutional-neural-networks)                 
<bar> [1.3.1 모델 설정](#build-the-model)               
<bar> [1.3.2 모델 학습](#train-the-model)                
<bar> [1.3.3 정확도 평가](#evaluate-accuracy)                   
<bar> [1.3.4 예측](#make-predictions)                  

[2. 운전 장면 분할](#driving-scene-segmentation)            
[2.1 모델 생성](#build-the-model)             
[2.2 시각화](#visualization)               
[2.3 고정 그래프에서 모델 로드](#load-the-model-from-a-frozen-graph)            
[2.4 샘플 이미지에서 실행](#run-on-the-sample-image)              
[2.5 샘플 비디오에서 실행](#run-on-the-sample-video)               
[2.6 평가](#evaluation)               
[2.7 샘플 이미지에 대한 평가](#evaluate-on-the-sample-image)             
[2.8 샘플 이미지에 대한 평가](#evaluate-on-the-sample-video)               
[2.9 선택사항 : 시간 정보 활용](#optional-leverage-temporal-information)             


[3. GAN (Generative Adversarial Network)](#generative-adversarial-metworks)      
[3.1 BigGAN](#biggan)

[4. DeepTraffic 심층 강화 학습 대회](#deeptraffic-deep-reinforcement-learning-competition)          

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

신경망 모델을 훈련하려면 다음 단계가 필요하다.

```markdown
1. 이 예에서는 train_image, train_label 배열과 같은 교육 데이터를 모델에 제공
2. 모델은 이미지와 레이블을 연결하는 방법을 배웁니다.
3. 이 예에서는 test_images 배열로 테스트 세트에 대해 예측하도록 모델에 요청한다. 그리고 예측이 test_labels 배열의 레이블과 일치하는지 검증한다.
```

학습이 시작되면 모델에게 교육데이터가 '적합'한지 확인한다.

```python
history = model.fit(train_images, train_labels, epochs=5)
```

### Evaluate accuracy

테스트 데이터 세트에서 모델의 성능을 비교한다.

```python
print(test_images.shape)
test_loss, test_acc = model.evaluate(test_images, test_labels)

print('Test accuracy:', test_acc)
```

종종 테스트 데이터 세트의 정확도가 교육 데이터 세트의 정확성보다 약간 떨어지는 경우가 있다. 훈련 정확도와 시험 정확도 사이의 이러한 차이는 과적합 사례이다. 우리의 경우 정확도가 99.19%로 더 우수하다. 이는 부분적으로 드롭아웃 계층에서 성공적으로 정규화가 이루어졌기 때문이다.

### Make predictions

훈련된 모델을 사용하여 일부 이미지에 대한 예측을 할 수 있다. 이를 위해 MNIST 데이터 세트를 벗어나 CPPN, GAN, VAE의 혼합으로 생성된 아름다운 고해상도 이미지로 이동해 보자. 원본 데이터와 이러한 변조된 애니메이션의 생성 방법에 대한 설명은 [하드마루 블로그 게시물](https://blog.otoro.net/2016/04/01/generating-large-images-from-latent-vectors/)을 참조하라.

![](https://camo.githubusercontent.com/fa61cfca07320919eb6430a2a06f98d3e68e29c1/68747470733a2f2f692e696d6775722e636f6d2f4f72554a7339562e676966)

```python
mnist_dream_path = 'images/mnist_dream.mp4'
mnist_prediction_path = 'images/mnist_dream_predicted.mp4'

# Colab에서 실행 중인 경우 영상 다운로드
if not os.path.isfile(mnist_dream_path): 
    print('downloading the sample video...')
    vid_url = this_tutorial_url + '/' + mnist_dream_path
    
    mnist_dream_path = urllib.request.urlretrieve(vid_url)[0]
                                                                                                  
def cv2_imshow(img):
    ret = cv2.imencode('.png', img)[1].tobytes() 
    img_ip = IPython.display.Image(data=ret)
    IPython.display.display(img_ip)

cap = cv2.VideoCapture(mnist_dream_path) 
vw = None
frame = -1 # 디버깅을 위한 카운터, 0-indexed

# 모든 프레임을 살펴보고 MNIST 영상에 대해 분류기를 실행(숫자에서 숫자로 형태 변환)
while True: # 481 프레임이어야 함
    frame += 1
    ret, img = cap.read()
    if not ret: break
               
    assert img.shape[0] == img.shape[1] # 정사각형이어야 한다
    if img.shape[0] != 720:
        img = cv2.resize(img, (720, 720))
       
    #preprocess the image for prediction
    img_proc = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    img_proc = cv2.resize(img_proc, (28, 28))
    img_proc = preprocess_images(img_proc)
    img_proc = 1 - img_proc # 교육 데이터 세트가 검정 바탕의 흰색 텍스트이므로 역방향

    net_in = np.expand_dims(img_proc, axis=0) # 차원을 확장하여 배치 크기를 1로 지정
    net_in = np.expand_dims(net_in, axis=3) # 차원을 확장하여 채널 수 지정
    
    preds = model.predict(net_in)[0]
    guess = np.argmax(preds)
    perc = np.rint(preds * 100).astype(int)
    
    img = 255 - img
    pad_color = 0
    img = np.pad(img, ((0,0), (0,1280-720), (0,0)), mode='constant', constant_values=(pad_color))  
    
    line_type = cv2.LINE_AA
    font_face = cv2.FONT_HERSHEY_SIMPLEX
    font_scale = 1.3        
    thickness = 2
    x, y = 740, 60
    color = (255, 255, 255)
    
    text = "Neural Network Output:"
    cv2.putText(img, text=text, org=(x, y), fontScale=font_scale, fontFace=font_face, thickness=thickness, color=color, lineType=line_type)
    
    text = "Input:"
    cv2.putText(img, text=text, org=(30, y), fontScale=font_scale, fontFace=font_face, thickness=thickness, color=color, lineType=line_type)   
        
    y = 130
    for i, p in enumerate(perc):
        if i == guess: color = (255, 218, 158)
        else: color = (100, 100, 100)
            
        rect_width = 0
        if p > 0: rect_width = int(p * 3.3)
        
        rect_start = 180
        cv2.rectangle(img, (x+rect_start, y-5), (x+rect_start+rect_width, y-20), color, -1)

        text = '{}: {:>3}%'.format(i, int(p))
        cv2.putText(img, text=text, org=(x, y), fontScale=font_scale, fontFace=font_face, thickness=thickness, color=color, lineType=line_type)
        y += 60
    
    # 출력을 비디오로 저장하지 않으려면 False로 설정
    save_video = True
    
    if save_video:
        if vw is None:
            codec = cv2.VideoWriter_fourcc(*'DIVX')
            vid_width_height = img.shape[1], img.shape[0]
            vw = cv2.VideoWriter(mnist_prediction_path, codec, 30, vid_width_height)
        # 위 15fps는 제대로 작동하지 않기 때문에 30fps에서 두 번 오른쪽으로 이동
        vw.write(img)
        vw.write(img)
    
    # 표시할 이미지를 축소
    img_disp = cv2.resize(img, (0,0), fx=0.5, fy=0.5)
    cv2_imshow(img_disp)
    IPython.display.clear_output(wait=True)
        
cap.release()
if vw is not None:
    vw.release()
```

![3](https://github.com/junsu9637/Study/blob/main/Artificial%20Intelligence/Montreal%20AI%20101%20-%20Cheet%20Sheet/Deep%20Learning/MIT-Deep%20Learning%20Review/Image/3.png?raw=true)

위의 내용은 출력이 가장 높은 뉴런을 선택하여 네트워크의 예측을 보여준다. 출력 계층 값이 1에 1을 추가하는 반면, 이 값들은 "불확도"의 잘 보정된 측정값을 반영하지 않는다. 종종, 네트워크는 학습된 확률 측정치를 반영하지 않는 최고 선택에 대해 지나치게 자신한다. 모든 것이 제대로 실행되었다면 다음과 같은 애니메이션을 얻을 수 있다. 

![](https://camo.githubusercontent.com/62ff651ca933abe4bc8468fc7035633f49e69235/68747470733a2f2f692e696d6775722e636f6d2f654d4639464f472e676966)

# Driving Scene Segmentation

이 문서는 MIT 드라이빙 장면 분할 데이터 세트의 샘플 비디오에서 DeepLab 의미 장면 분할 모델을 실행하는 단계를 시연한다.

```python
# Tensorflow
import tensorflow as tf
print(tf.__version__)

# I/O libraries
import os
from io import BytesIO
import tarfile
import tempfile
from six.moves import urllib

# Helper libraries
import matplotlib
from matplotlib import gridspec
from matplotlib import pyplot as plt
import numpy as np
from PIL import Image
import cv2 as cv
from tqdm import tqdm
import IPython
from sklearn.metrics import confusion_matrix
from tabulate import tabulate

# 경고를 보려면 이 설명을 참조(잘 사용 안 함)
import warnings
warnings.simplefilter("ignore", DeprecationWarning)
```

## Build the model

DeepLab은 의미론적 이미지 분할을 위한 최첨단 Deep Learning 모델로, 여기서 목표는 입력 이미지의 모든 픽셀에 의미론적 레이블(예: 사람, 개, 고양이 등)을 할당하는 것이다. Flickr 영상의 일부 분할 결과는 아래와 같다.

![](https://camo.githubusercontent.com/a59b7e7c6dd1744c85fc667cf48aec022365b103/68747470733a2f2f6769746875622e636f6d2f74656e736f72666c6f772f6d6f64656c732f626c6f622f6d61737465722f72657365617263682f646565706c61622f6733646f632f696d672f766973312e706e673f7261773d74727565)

운전의 맥락에서, 우리는 카메라 입력을 통해 전방 주행 장면에 대한 의미적 이해를 얻는 것을 목표로 한다. 이는 운전 안전에 중요하며 모든 수준의 자율 주행에 필수적인 요건이다. 첫 번째 단계는 모델을 작성하고 사전 훈련된 가중치를 로드하는 것이다. 이 데모에서는 Cityscapes 데이터 세트에 대해 훈련된 모델 체크포인트를 사용한다.

![](https://camo.githubusercontent.com/131d89bfcabd56e73216e70c78dedd0cb3203374/68747470733a2f2f7777772e636974797363617065732d646174617365742e636f6d2f776f726470726573732f77702d636f6e74656e742f75706c6f6164732f323031352f30372f6d75656e7374657230302e706e67)

![](https://camo.githubusercontent.com/9f6b59d72d4175f9dccf245ec56c0b2c131ccf55/68747470733a2f2f7777772e636974797363617065732d646174617365742e636f6d2f776f726470726573732f77702d636f6e74656e742f75706c6f6164732f323031352f30372f7a75657269636830302e706e67)

```python
class DeepLabModel(object):
    """Deeplab 모델을 로드하고 추론을 실행할 클래스"""

    FROZEN_GRAPH_NAME = 'frozen_inference_graph'

    def __init__(self, tarball_path):
        """사전 훈련된 Deeplab 모델 생성 및 로드"""
        self.graph = tf.Graph()
        graph_def = None

        # tar 아카이브에서 고정 그래프를 추출
        tar_file = tarfile.open(tarball_path)
        for tar_info in tar_file.getmembers():
            if self.FROZEN_GRAPH_NAME in os.path.basename(tar_info.name):
                file_handle = tar_file.extractfile(tar_info)
                graph_def = tf.GraphDef.FromString(file_handle.read())
                break
        tar_file.close()

        if graph_def is None:
            raise RuntimeError('Cannot find inference graph in tar archive.')

        with self.graph.as_default():
            tf.import_graph_def(graph_def, name='')
        self.sess = tf.Session(graph=self.graph)

    def run(self, image, INPUT_TENSOR_NAME = 'ImageTensor:0', OUTPUT_TENSOR_NAME = 'SemanticPredictions:0'):
        """단일 이미지에서 추론 실행

        Args:
            image: A PIL.Image 개체로 원시 입력 이미지
            INPUT_TENSOR_NAME: 입력 텐서의 이름(기본 값 : ImageTensor)
            OUTPUT_TENSOR_NAME: 입력 텐서의 이름으로 의미론적 예측으로 설정

        Returns:
            resized_image: 원래 입력 이미지에서 크기가 조정된 RGB 이미지
            seg_map: 'resize_image'의 분할 맵
        """
        width, height = image.size
        target_size = (2049,1025)  # Cityscapes images의 크기
        resized_image = image.convert('RGB').resize(target_size, Image.ANTIALIAS)
        batch_seg_map = self.sess.run(
            OUTPUT_TENSOR_NAME,
            feed_dict={INPUT_TENSOR_NAME: [np.asarray(resized_image)]})
        seg_map = batch_seg_map[0]  # expected batch size = 1
        if len(seg_map.shape) == 2:
            seg_map = np.expand_dims(seg_map,-1)  # cv.resize를 위한 추가 자원 필요
        seg_map = cv.resize(seg_map, (width,height), interpolation=cv.INTER_NEAREST)
        return seg_map
```

## Visualization

결과를 디코딩하고 시각화하기 위한 몇 가지 도우미 기능을 만들어보자.

```python
def create_label_colormap():
    """세그먼트 된 밴치마크인 Cityscapes를 사용하여 색상 맵 레이블 생성

    Returns:
        분할 결과를 시각화하기 위한 색상 맵
    """
    colormap = np.array([
        [128,  64, 128],
        [244,  35, 232],
        [ 70,  70,  70],
        [102, 102, 156],
        [190, 153, 153],
        [153, 153, 153],
        [250, 170,  30],
        [220, 220,   0],
        [107, 142,  35],
        [152, 251, 152],
        [ 70, 130, 180],
        [220,  20,  60],
        [255,   0,   0],
        [  0,   0, 142],
        [  0,   0,  70],
        [  0,  60, 100],
        [  0,  80, 100],
        [  0,   0, 230],
        [119,  11,  32],
        [  0,   0,   0]], dtype=np.uint8)
    return colormap


def label_to_color_image(label):
    """분할 결과를 시각화하기 위한 색상 맵으로 데이터 세트 색상 맵에 의해 정의된 색상을 레이블에 추가

    Args:
        label: 정수 유형의 2D 배열로 분할 레이블을 저장

    Returns:
        result: 실수 형식의 2D 배열이다. 배열 요소는 PASCAL 색상 맵에 대한 입력 레이블의 해당 요소에 의해 인덱싱된 색상이다. 

    Raises:
        ValueError: 라벨이 2등급이 아니거나 라벨의 값이 색상 맵 최대 항목보다 큰 경우
    """
    if label.ndim != 2:
        raise ValueError('Expect 2-D input label')

    colormap = create_label_colormap()

    if np.max(label) >= len(colormap):
        raise ValueError('label value too large.')

    return colormap[label]


def vis_segmentation(image, seg_map):
    """입력 이미지, 분할 지도, 오버레이를 시각화"""
    plt.figure(figsize=(20, 4))
    grid_spec = gridspec.GridSpec(1, 4, width_ratios=[6, 6, 6, 1])

    plt.subplot(grid_spec[0])
    plt.imshow(image)
    plt.axis('off')
    plt.title('input image')

    plt.subplot(grid_spec[1])
    seg_image = label_to_color_image(seg_map).astype(np.uint8)
    plt.imshow(seg_image)
    plt.axis('off')
    plt.title('segmentation map')

    plt.subplot(grid_spec[2])
    plt.imshow(image)
    plt.imshow(seg_image, alpha=0.7)
    plt.axis('off')
    plt.title('segmentation overlay')

    unique_labels = np.unique(seg_map)
    ax = plt.subplot(grid_spec[3])
    plt.imshow(FULL_COLOR_MAP[unique_labels].astype(np.uint8), interpolation='nearest')
    ax.yaxis.tick_right()
    plt.yticks(range(len(unique_labels)), LABEL_NAMES[unique_labels])
    plt.xticks([], [])
    ax.tick_params(width=0.0)
    plt.grid('off')
    plt.show()


LABEL_NAMES = np.asarray([
    'road', 'sidewalk', 'building', 'wall', 'fence', 'pole', 'traffic light', 'traffic sign', 'vegetation', 'terrain', 'sky', 'person', 'rider', 'car', 'truck', 'bus', 'train', 'motorcycle', 'bicycle', 'void'])

FULL_LABEL_MAP = np.arange(len(LABEL_NAMES)).reshape(len(LABEL_NAMES), 1)
FULL_COLOR_MAP = label_to_color_image(FULL_LABEL_MAP)
```

## Load the model from a frozen graph

다양한 네트워크 기반이 있는 Cityscape에 대해 사전 교육을 받은 두 가지 모델 체크포인트(MobileNetV2, Xception65)가 있다. 우리는 더 빠른 추론을 위해 MobileNetV2를 기본적으로 사용한다.

```python
MODEL_NAME = 'mobilenetv2_coco_cityscapes_trainfine'
#MODEL_NAME = 'xception65_cityscapes_trainfine'

_DOWNLOAD_URL_PREFIX = 'http://download.tensorflow.org/models/'
_MODEL_URLS = {'mobilenetv2_coco_cityscapes_trainfine':'deeplabv3_mnv2_cityscapes_train_2018_02_05.tar.gz', 'xception65_cityscapes_trainfine':'deeplabv3_cityscapes_train_2018_02_06.tar.gz',}
_TARBALL_NAME = 'deeplab_model.tar.gz'

model_dir = tempfile.mkdtemp()
tf.gfile.MakeDirs(model_dir)

download_path = os.path.join(model_dir, _TARBALL_NAME)
print('downloading model, this might take a while...')
urllib.request.urlretrieve(_DOWNLOAD_URL_PREFIX + _MODEL_URLS[MODEL_NAME], download_path)
print('download completed! loading DeepLab model...')

MODEL = DeepLabModel(download_path)
print('model loaded successfully!')
```

## Run on the sample image

샘플 이미지는 MIT 주행 장면 분할(DriveSeg) 데이터 세트의 프레임이다(0).

```python
SAMPLE_IMAGE = 'mit_driveseg_sample.png'
if not os.path.isfile(SAMPLE_IMAGE):
    print('downloading the sample image...')
    SAMPLE_IMAGE = urllib.request.urlretrieve('https://github.com/lexfridman/mit-deep-learning/blob/master/tutorial_driving_scene_segmentation/mit_driveseg_sample.png?raw=true')[0]
print('running deeplab on the sample image...')

def run_visualization(SAMPLE_IMAGE):
    """Inferences DeepLab model and visualizes result."""
    original_im = Image.open(SAMPLE_IMAGE)
    seg_map = MODEL.run(original_im)
    vis_segmentation(original_im, seg_map)

run_visualization(SAMPLE_IMAGE)
```

![](https://github.com/junsu9637/Study/blob/main/Artificial%20Intelligence/Montreal%20AI%20101%20-%20Cheet%20Sheet/Deep%20Learning/MIT-Deep%20Learning%20Review/Image/4.png?raw=true)

## Run on the sample video

샘플 비디오는 MIT DriveSeg 데이터 세트에서 프레임이다(0~597). 

```python
def vis_segmentation_stream(image, seg_map, index):
    """분할 오버레이를 시각화하여 IPython 디스플레이로 스트리밍"""
    plt.figure(figsize=(12, 7))

    seg_image = label_to_color_image(seg_map).astype(np.uint8)
    plt.imshow(image)
    plt.imshow(seg_image, alpha=0.7)
    plt.axis('off')
    plt.title('segmentation overlay | frame #%d'%index)
    plt.grid('off')
    plt.tight_layout()

    # Show visualization in a streaming fashion.
    f = BytesIO()
    plt.savefig(f, format='jpeg')
    IPython.display.display(IPython.display.Image(data=f.getvalue()))
    f.close()
    plt.close()


def run_visualization_video(frame, index):
    """비디오 파일에서 DeepLab 모델을 추론하고 시각화를 스트리밍"""
    original_im = Image.fromarray(frame[..., ::-1])
    seg_map = MODEL.run(original_im)
    vis_segmentation_stream(original_im, seg_map, index)


SAMPLE_VIDEO = 'mit_driveseg_sample.mp4'
if not os.path.isfile(SAMPLE_VIDEO): 
    print('downloading the sample video...')
    SAMPLE_VIDEO = urllib.request.urlretrieve('https://github.com/lexfridman/mit-deep-learning/raw/master/tutorial_driving_scene_segmentation/mit_driveseg_sample.mp4')[0]
print('running deeplab on the sample video...')

video = cv.VideoCapture(SAMPLE_VIDEO)
# num_frames = 598  # 전체 샘플 비디오를 사용하기 위해 사용
num_frames = 30

try:
    for i in range(num_frames):
        _, frame = video.read()
        if not _: break
        run_visualization_video(frame, i)
        IPython.display.clear_output(wait=True)
except KeyboardInterrupt:
    plt.close()
    print("Stream stopped.")
```

![5](https://github.com/junsu9637/Study/blob/main/Artificial%20Intelligence/Montreal%20AI%20101%20-%20Cheet%20Sheet/Deep%20Learning/MIT-Deep%20Learning%20Review/Image/5.png?raw=true)

## Evaluation

이제 실측 주석을 사용하여 모델 성능을 평가해보자. 먼저 tar 파일에서 주석을 읽는다. 

```python
class DriveSeg(object):
    """MIT DriveSeg 데이터 세트를 로드하는 클래스"""

    def __init__(self, tarball_path):
        self.tar_file = tarfile.open(tarball_path)
        self.tar_info = self.tar_file.getmembers()
    
    def fetch(self, index):
        """지수를 기준으로 실측을 구한다.

        Args:
            index: 프레임 개수.

        Returns:
            gt: 실측 분할 맵
        """
        tar_info = self.tar_info[index + 1]  # 상위 디렉토리인 인덱스 0 제외
        file_handle = self.tar_file.extractfile(tar_info)
        gt = np.fromstring(file_handle.read(), np.uint8)
        gt = cv.imdecode(gt, cv.IMREAD_COLOR)
        gt = gt[:, :, 0]  # 3채널 이미지에서 단일 채널 선택
        gt[gt==255] = 19 
        return gt


SAMPLE_GT = 'mit_driveseg_sample_gt.tar.gz'
if not os.path.isfile(SAMPLE_GT): 
    print('downloading the sample ground truth...')
    SAMPLE_GT = urllib.request.urlretrieve('https://github.com/lexfridman/mit-deep-learning/raw/master/tutorial_driving_scene_segmentation/mit_driveseg_sample_gt.tar.gz')[0]

dataset = DriveSeg(SAMPLE_GT)
print('visualizing ground truth annotation on the sample image...')

original_im = Image.open(SAMPLE_IMAGE)
gt = dataset.fetch(0)  # 샘플 이미지는 프레임 0
vis_segmentation(original_im, gt)
```
![6](https://github.com/junsu9637/Study/blob/main/Artificial%20Intelligence/Montreal%20AI%20101%20-%20Cheet%20Sheet/Deep%20Learning/MIT-Deep%20Learning%20Review/Image/6.png?raw=true)

## Evaluate on the sample image

분할 모델의 성능을 측정하는 방법은 여러 가지가 있다. 가장 직설적인 것은 픽셀 정확도로 얼마나 많은 픽셀이 정확하게 예측되는지를 계산한다. 일반적으로 사용되는 또 다른 Jaccard Index(교차 초과 결합)는 IoU = TP α(TP+FP+FN)이다. 여기서 TP, FP 및 FN은 각각 참 양, 거짓 양 및 거짓 음의 픽셀 수다. 

```python
def evaluate_single(seg_map, ground_truth):
    """모델이 로드된 상태에서 단일 프레임을 평가"""    
    # merge label due to different annotation scheme
    seg_map[np.logical_or(seg_map==14,seg_map==15)] = 13
    seg_map[np.logical_or(seg_map==3,seg_map==4)] = 2
    seg_map[seg_map==12] = 11

    # 유효 면적의 정확도를 계산
    acc = np.sum(seg_map[ground_truth!=19]==ground_truth[ground_truth!=19])/np.sum(ground_truth!=19)
    
    # 평가를 위한 유효한 레이블 선택
    cm = confusion_matrix(ground_truth[ground_truth!=19], seg_map[ground_truth!=19], 
                          labels=np.array([0,1,2,5,6,7,8,9,11,13]))
    intersection = np.diag(cm)
    union = np.sum(cm, 0) + np.sum(cm, 1) - np.diag(cm)
    return acc, intersection, union


print('evaluating on the sample image...')

original_im = Image.open(SAMPLE_IMAGE)
seg_map = MODEL.run(original_im)
gt = dataset.fetch(0)  # 샘플 이미지는 프레임 0
acc, intersection, union = evaluate_single(seg_map, gt)
class_iou = np.round(intersection / union, 5)
print('pixel accuracy: %.5f'%acc)
print('mean class IoU:', np.mean(class_iou))
print('class IoU:')
print(tabulate([class_iou], headers=LABEL_NAMES[[0,1,2,5,6,7,8,9,11,13]]))
```

## Evaluate on the sample video

```python
print('evaluating on the sample video...', flush=True)

video = cv.VideoCapture(SAMPLE_VIDEO)
# num_frames = 598 
num_frames = 30

acc = []
intersection = []
union = []

for i in tqdm(range(num_frames)):
    _, frame = video.read()
    original_im = Image.fromarray(frame[..., ::-1])
    seg_map = MODEL.run(original_im)
    gt = dataset.fetch(i)
    _acc, _intersection, _union = evaluate_single(seg_map, gt)
    intersection.append(_intersection)
    union.append(_union)
    acc.append(_acc)

class_iou = np.round(np.sum(intersection, 0) / np.sum(union, 0), 4)
print('pixel accuracy: %.4f'%np.mean(acc))
print('mean class IoU: %.4f'%np.mean(class_iou))
print('class IoU:')
print(tabulate([class_iou], headers=LABEL_NAMES[[0,1,2,5,6,7,8,9,11,13]]))
```

## Optional leverage temporal information

비디오 장면 분할을 이미지 분할과 다르게 만드는 한 가지는 지각에 도움이 될 수 있는 귀중한 시간 정보를 포함하는 이전 프레임의 가용성이다. 여기서 문제는 우리가 어떻게 그러한 시간적 정보를 사용할 수 있는가 하는 것이다. 한 프레임만 예측하지 않고 두 프레임의 예측을 결합하여 시간이 지남에 따라 보다 부드러운 예측을 만들어 보자.

```python
print('evaluating on the sample video with temporal smoothing...', flush=True)

video = cv.VideoCapture(SAMPLE_VIDEO)
# num_frames = 598  # uncomment to use the full sample video
num_frames = 30

acc = []
intersection = []
union = []
prev_seg_map_logits = 0

for i in tqdm(range(num_frames)):
    _, frame = video.read()
    original_im = Image.fromarray(frame[..., ::-1])
    
    # 레이블 예측 대신 로짓 가져오기
    seg_map_logits = MODEL.run(original_im, OUTPUT_TENSOR_NAME='ResizeBilinear_3:0')
    
    # 이전 프레임의 로짓 추가 및 결과 가져오기
    seg_map = np.argmax(seg_map_logits + prev_seg_map_logits, -1)
    prev_seg_map_logits = seg_map_logits
    
    gt = dataset.fetch(i)
    _acc, _intersection, _union = evaluate_single(seg_map, gt)
    intersection.append(_intersection)
    union.append(_union)
    acc.append(_acc)
    
class_iou = np.round(np.sum(intersection, 0) / np.sum(union, 0), 4)
print('pixel accuracy: %.4f'%np.mean(acc))
print('mean class IoU: %.4f'%np.mean(class_iou))
print('class IoU:')
print(tabulate([class_iou], headers=LABEL_NAMES[[0,1,2,5,6,7,8,9,11,13]]))
```

# Generative Adversarial Networks

이 문서는 MIT Deep Learning 시리즈 중 GAN에 대한 소개 강의를 기반으로 제작되었다.

GAN(Generative Adversarial Networks)은 특정 표현에서 새로운 실제 샘플을 생성하기 위해 최적화된 네트워크를 훈련하기 위한 프레임워크이다. 가장 간단한 형태로 훈련 과정은 두 개의 네트워크를 포함한다. generator이라고 불리는 하나의 내트워크는 새 인스턴스를 생성한다. 이 인스턴스는 다른 네트워크를 속이고 이미지를 실제 또는 가짜로 분류한다. 

![](https://camo.githubusercontent.com/8415e3ee30cee611cf88eabee12eac47da54c110/68747470733a2f2f692e696d6775722e636f6d2f4c7765614431732e706e67)

GAN에는 대략 3가지 범주가 있다.

> **비지도 GANs**          
  generator 네트워크는 무작위 노이즈를 입력으로 받아들이고, 교육 데이터 세트에 나타나는 이미지와 유사한 이미지를 생성한다.         
  **스타일 전송 GAN**         
  한 영역에서 다른 영역으로 이미지 변환(예: 말에서 얼룩말)         
  **조건부 GAN**         
  이미지와 함께 특징에 대해 공동으로 학습하여 해당 특징에 따라 조건화된 이미지를 생성한다(예: 특정 클래스의 인스턴스 생성)
  
본 문서에서는 먼저 DeepMind의 최첨단 조건부 GAN인 BigGAN을 설명한다. 이 그림은 BigGAN TF Hub Demo와 TF Hub의 BigGAN 생성기를 기반으로 만들어 졌다. 

## BigGAN

```python
# 기본
import io
import os
import numpy as np

# Deep Learning
from scipy.stats import truncnorm
import tensorflow as tf
import tensorflow_hub as hub

# 시각화
from IPython.core.display import HTML
#!pip install imageio
import imageio
import base64

# TensorFlow GPU가 활성화되어 있는지 확인
tf.test.gpu_device_name() # returns empty string if using CPU
```

**TF Hub에서 BigGAN generator 모듈 로드**
```python
# 사용할 TF Hub 모듈 경로를 설명
# module_path = 'https://tfhub.dev/deepmind/biggan-128/1'  # 128x128 BigGAN
# module_path = 'https://tfhub.dev/deepmind/biggan-256/1'  # 256x256 BigGAN
module_path = 'https://tfhub.dev/deepmind/biggan-512/1'  # 512x512 BigGAN

tf.reset_default_graph()
print('Loading BigGAN module from:', module_path)
module = hub.Module(module_path)
inputs = {k: tf.placeholder(v.dtype, v.get_shape().as_list(), k)
          for k, v in module.get_input_info_dict().items()}
output = module(inputs)
```

**generator 샘플링 및 보간 기능**
```python
input_z = inputs['z']
input_y = inputs['y']
input_trunc = inputs['truncation']

dim_z = input_z.shape.as_list()[1]
vocab_size = input_y.shape.as_list()[1]

# 표본을 잘라내는 매개 변수를 기반으로 한 정규 분포
def truncated_z_sample(truncation=1., seed=None):
    state = None if seed is None else np.random.RandomState(seed)
    values = truncnorm.rvs(-2, 2, size=(1, dim_z), random_state=state)
    return truncation * values

# 인덱스 값을 인덱스 1을 제외한 모든 0의 벡터로 변환
def one_hot(index, vocab_size=vocab_size):
    index = np.asarray(index)
    if len(index.shape) == 0: # 크기가 1인 벡터로 변환될 때
        index = np.asarray([index])
    assert len(index.shape) == 1
    num = index.shape[0]
    output = np.zeros((num, vocab_size), dtype=np.float32)
    output[np.arange(num), index] = 1
    return output

def one_hot_if_needed(label, vocab_size=vocab_size):
    label = np.asarray(label)
    if len(label.shape) <= 1:
        label = one_hot(label, vocab_size)
    assert len(label.shape) == 2
    return label

# 노이즈 시드 및 범주 레이블의 벡터 사용, 이미지 생성
def sample(sess, noise, label, truncation=1., batch_size=8, vocab_size=vocab_size):
    noise = np.asarray(noise)
    label = np.asarray(label)
    num = noise.shape[0]
    if len(label.shape) == 0:
        label = np.asarray([label] * num)
    if label.shape[0] != num:
        raise ValueError('Got # noise samples ({}) != # label samples ({})'
                         .format(noise.shape[0], label.shape[0]))
    label = one_hot_if_needed(label, vocab_size)
    ims = []
    for batch_start in range(0, num, batch_size):
        s = slice(batch_start, min(num, batch_start + batch_size))
        feed_dict = {input_z: noise[s], input_y: label[s], input_trunc: truncation}
        ims.append(sess.run(output, feed_dict=feed_dict))
    ims = np.concatenate(ims, axis=0)
    assert ims.shape[0] == num
    ims = np.clip(((ims + 1) / 2.0) * 256, 0, 255)
    ims = np.uint8(ims)
    return ims

def interpolate(a, b, num_interps):
    alphas = np.linspace(0, 1, num_interps)
    assert a.shape == b.shape, 'A and B must have the same shape to interpolate.'
    return np.array([(1-x)*a + x*b for x in alphas])

def interpolate_and_shape(a, b, steps):
    interps = interpolate(a, b, steps)
    return (interps.transpose(1, 0, *range(2, len(interps.shape))).reshape(steps, -1))
```

**TensorFlow 세션 생성 및 변수 초기화**
```python
initializer = tf.global_variables_initializer()
sess = tf.Session()
sess.run(initializer)
```

**보간된 BigGAN 생성기 샘플의 비디오 생성**
```python
# category options: https://gist.github.com/yrevar/942d3a0ac09ec9e5eb3a
category = 947 # 버섯 이미지

# 변동량을 제어하는 중요 매개변수
truncation = 0.2 # 적당한 범위: [0.02, 1]

seed_count = 10
clip_secs = 36

seed_step = int(100 / seed_count)
interp_frames = int(clip_secs * 30 / seed_count)  # 보간 프레임

cat1 = category
cat2 = category
all_imgs = []

for i in range(seed_count):
    seed1 = i * seed_step # 좋은 시드 범위는 [0, 100]이다.
    seed2 = ((i+1) % seed_count) * seed_step
    
    z1, z2 = [truncated_z_sample(truncation, seed) for seed in [seed1, seed2]]
    y1, y2 = [one_hot([category]) for category in [cat1, cat2]]

    z_interp = interpolate_and_shape(z1, z2, interp_frames)
    y_interp = interpolate_and_shape(y1, y2, interp_frames)

    imgs = sample(sess, z_interp, y_interp, truncation=truncation)
    
    all_imgs.extend(imgs[:-1])

# 비디오를 저장하여 다음 셀에 표시(gif 애니메이션보다 공간 효율적)
imageio.mimsave('gan.mp4', all_imgs, fps=30)
```

![](https://camo.githubusercontent.com/5076c943634ca412b813d55421a2ce857a96dc33/68747470733a2f2f692e696d6775722e636f6d2f544139756831612e676966)

# DeepTraffic Deep Reinforcement Learning Competition
