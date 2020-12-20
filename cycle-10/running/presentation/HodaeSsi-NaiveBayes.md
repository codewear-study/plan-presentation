# 나이브 베이즈 분류기(Naive Bayes  Classifier)

### 1. 베이즈 정리

- 베이즈 정리(Bayes' theorem)
  : "조건부 확률의 계산"
  $$
  p(A|B) = \frac{p(A,B)}{p(B)} = \frac{p(B|A)p(A)}{p(B)}
  $$
  : 단순히 표본을 통해 추정하는 것이 아닌, **사전 확률 및 사전 정보를 기반으로 사후 확률을 추론하는 통계적 기법**

- 예시

  1. 어떤 마을의 10.5%는 암 환자이다. 

     > p(C) = 0.105, p(~C) = 0.895

  2. 암 검진이 오차가 있다고 했을 때, 암 환자에게 양성 판정을 내릴 확률은 90.5% 

     > p(P|C) = 0.905, p(N|C) = 0.095

  3. 암 환자가 _아닌_ 사람에게 양성 판정을 내릴 확률은 20.4%

     > p(P|~C) = 0.204, p(N|~C) = 0.796

  이때 p(C|P), 즉 양성 판정을 받은 사람이 암 환자일 확률은?
  $$
  p(C|P) = \frac{p(P|C)p(C)}{p(P)}
  $$
  여기서, 
  $$
  p(P) = p(P,C) + P(P,C^c) = p(P|C)*p(C) + p(P|C^c)*p(C^c)
  $$
  그러므로,
  $$
  p(C|P) = \frac{0.905*0.105}{0.905*0.105+0.204*0.895}=0.342
  $$

### 2. 나이브 베이즈 분류기 - 이론

- Feature(속성)와 Label(라벨)
  ex) 스펨 메일 분류
  	Label : 스펨 메일인가(1), 아닌가(0)

  ​	Feature : 메일에 포함된 광고성 단어의 개수, 비속의 개수, ...

- 지도학습(Supervised Learning)

  ![surpervised learning process](https://miro.medium.com/max/1400/1*SS51laVNAHEXIcJDyHk3iw.png)

- 장/단점, 사용하는 곳

  - 장점

    1. (비교적) 간단하고, 빠르며, 정확한 수준의 모델
    2. 큰 데이터셋에 적합
    3. 연속형 데이터 보다는 이산형 데이터에 성능이 좋음

  - 단점

    1. feature간 독립성이 있어야 함(하지만 현실은...)

  - 사용

    ​	1.스팸 메일 필터, 텍스트 분류, 감정 분석, 추천 시스템, ...

- 예시
  pass

### 3. 나이브 베이즈 분류기 - 적용

- Python_scikit-learn라이브러리의 나이브 베이즈 분류기("모델") 종류

  1. GaussianNB - 연속적인 데이터에 적용
  2. BernoulliNB - 이진 분류에 사용
  3. MultinomiaNB - 다중 분류에 사용

- 적용 예시(GaussianNB)

  "날씨와 온도에 따라 야구 경기가 진행될지 여부를 예측하는 인공지능을 만들어 보자"

  1. 데이터(train) 준비

     > weather = ['Sunny', 'Overcast', 'Rainy', ... ] #feature_1
     >
     > temp = ['Hot', 'Mild', 'Cool', ... ] #feature_2
     >
     > play = ['No', 'Yes', ... ] #label

  2. 데이터 인코딩(string > int)

     ```python
     from sklearn import preprocesisng
     
     LE = preprocessing.LabelEncoder()
     weather_encoded = LE.fit_transform(weather)
     temp_encoded = LE.fit_transform(temp)
     label = LE.fit_transform(play)
     
     print(weather_encoded)
     ```

      ```
     >>> [0 1 2 2 1 ... ]
      ```

  3. feature 결합

     ```python
     features = zip(weather_encoded, temp_encoded)
     features = list(features)
     print(features)
     ```

     ```
     >>> [(2, 1), (1, 2), (0, 2), ... ]
     ```

  4. 분류기 제작(모델 생성 > 훈련 데이터 학습 > 테스트(평가))

     ```python
     from sklearn.naive_bayes import GaussianNB
     
     naiveModel = GaussianNB()
     
     model.fit(features, label)
     
     predicted = naiveModel.predict([0, 2])
     print("Predicted Value: ", predicted)
     ```

     ```
     Predicted Value: (Play Or !Play)
     ```

     