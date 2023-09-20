# Machine Learning
1. Supervised Learning(지도학습) : 타겟(답, label)이 있다.  &rarr; 예측 모델 생성
 -  Regression(수치예측)
 -  Classification(범주예측)
<br>
&rarr; error를 줄이는 방향으로 학습이 진행될 것임을 추측할 수 있다.
<br>
2. Unsupervised Learning(비지도학습) : 타겟(답, label)이 없다.
 - Clustering(군집, 차원축소)

<br><br>

## Gradient Descent(경사 하강법)
- 목적 : 학습(Learning, Parameter의 Update되는 순간)의 자동화
- 예측값이 실제값과 가까운 값이 나오도록 parameter(w:가중치, b:오차 및 편향값)을 조절.
  <br>
    ![위키백과-회귀분석](https://upload.wikimedia.org/wikipedia/commons/b/be/Normdist_regression.png)
  <br>
- 실제값 - 예측값 = Error : 에러값이 작을 수록 좋다.
- 따라서 Mean Squared Error(MSE)가 작을 수록 좋다

    <img src="https://machinelearningspace.com/wp-content/uploads/2023/01/Gradient-Descent-Top2-1024x645.png" width="500"><br>
- weight와 bias의 값을 변경시킬 때마다 MSE의 값은 줄어들거나 증가된다. 이것을 형상화하면 위의 그림과 같다.
- 즉, weight-MSE, bias-MSE의 관계를 형상화하면 2차 함수가 나온다!<br>
    <img src="https://sebastianraschka.com/images/faq/gradient-optimization/ball.png" width="500">
    ![ibm](https://www.ibm.com/content/dam/connectedassets-adobe-cms/worldwide-content/cdp/cf/ul/g/c2/0f/ICLH_Diagram_Batch_03_21-AI-ML-GradientDescent.component.simple-narrative-xl-retina.ts=1694450696234.png/content/adobe-cms/us/en/topics/gradient-descent/jcr:content/root/table_of_contents/body/content_section_styled/content-section-body/simple_narrative_1771421240/image)

- 하지만 단순하게 최소값이 하나만 있지 않다. Gradient Descent는 실제로 아래와 같이 생겼다.<br>
    <img src="https://easyai.tech/wp-content/uploads/2019/01/tiduxiajiang-1.png" width="500">

<br><br>

## Model Validation(모델 검증)
모델을 사용하기에 적합한가를 확인한다. &rarr; 미래에 발생할 에러가 작아야 한다는 의미이다.
- 여러 모델을 만들어서 어떤 모델이 더 적합한지를 평가한다.  &rarr; MSE를 이용해서 판단

1. Model Capacity
   - 모델이 데이터의 분포를 얼마나 잘 설명/표현하고 있는가?

2. Training(=Learning) Error
   - 기본적으로 학습은 Training Error를 최소화하는 방향으로 진행한다.
   - Training Data에 Model을 적용해서 확인한 실제값과 예측값의 차이 &rarr; MSE

3. Overfitting(과적합) : 학습 결과가 Training Data에만 최적화된 모델을 생성한다. 따라서 모델 생성 시 사용하지 않은 Data에서 급격한 성능 저하 발생.

4. Testing Error : 예측 모델 학습 후 반드시 평가 필요
   - Training Data : 학습(모델 생성)을 위해 제공되는 데이터
   - Testing Data : 학습 결과를 평가(모델 평가)하기 위해 제공되는 데이터 