## 태양광 발전량 예측 프로젝트

* 동서발전에서 개최한 태양광 발전량 예측 공모전
* 주어진 기상데이터(외부데이터 사용 가능)로 울산에 하나, 당진에 세개 발전소에 대한 태양광 발전량 예측 모델을 만드는 것 
* 2018년 3월에서 2021년 1월말까지 1시간 단위로 측정 된 데이터

***

## 프로젝트 개요

* 외부데이터로 기존에 없던 일사, 일조, 대기오염물질, 강수량 데이터를 추가적으로 수집
* 계절변수, 강수량 범주화 등 파생변수 생성(결측값이 날은 동일하게 채워주기)
* 변수들의 결측치 처리는 회귀, KNN, 보간법을 사용
* 모델링 과정에서는 전운량 예측, 발전량 예측 두가지의 모델링 사용
* 전운량 모델링에서는 모든 기상데이터 변수를 사용했고 알고리즘은 랜덤포레스트를 사용
* 발전량 예측 모델링도 현재까지는 랜덤포레스트로 사용

***

## 전처리 과정

#### - 미세먼지 데이터는 25632개 중 1300개 가량의 결측치 존재

![img](https://lh4.googleusercontent.com/c5Eg7aPKdLpY2bmLYmjXYuUjjK9NTFbT7aI-VvVLKelsjD58rnONzhSzHfLHSgTcWXNsAn8NZSLvwqzRsP37oa8k7kCXpdIFElF_R_MD8pRlHEowuv2I6hKOeDSkYNTt)

![img](https://lh4.googleusercontent.com/DY8jSrLNhGuFTgP_I80ze3cQ0qC7lIb-tqt-1q3y-Y9nxzF-YDuSUXP44Kc_tF_ga6eC-XFZPC6d3ox65eBJO6BI0ZxzyIiWY432EZ0w7s60lFwkfBDkRN4S2mTYbfF6)

* 대기정보의 결측치를 2차보간으로 채웠을 때 분류기의 오차가 크게 나타남

* 결과적으로 KNN으로 결측치 처리

  

#### - 변수간의 상관분석

![img](https://lh3.googleusercontent.com/b2db0rNRq1SjBXRzs4DqNigW9lJlsyGrSnmSxHOVxcrQGhyc4YLJyQOPKlcGcpqlk5WRHUO9hdAKLSZXDl5oBTJpy_i_N6dv90iCLuWGUzwGU6Dbyi8VD7EZ7ZqFk6Sz)

* 상관분석을 통해 습도, 일사량, 일조시간, 오존지수가 선형상관관계를 띄는 발전량의 중요 변수임을 파악

## 결과 및 개선방법

* 전운량 예측을 할 때 피처의 중요도가 큰 온도와 강수량이 어떻게 모델링에 반영이 되었는지 decision boundary를 나타냈는데 정확도가 높지 않아서 bourdary가 명확하게 분리되지 않음

  ![result](README.assets/result.png)

  

* 각각 전운량:48.3%, 발전량:54% 의 정확도 산출

* test보다 train 데이터의 정확도가 높아서 모델의 오버피팅을 염두

* 0으로 편중된 값이 많아 이상치 처리가 미흡해 이 점을 보완하기 위해 IQR 이용 염두

* 자외선이나 강설량같은 추가적 변수도 고려해 정확도를 높일 수 있을 것이라고 생각

* 다양한 회귀모델을 사용하여 정확도 높일 수 있음

  
