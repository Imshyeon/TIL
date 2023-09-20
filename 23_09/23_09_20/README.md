# Machine Learning
1. Supervised Learning(지도학습) : 타겟(답, label)이 있다.
 -  Regression(수치예측)
 -  Classification(범주예측)
<br>
&rarr; error를 줄이는 방향으로 학습이 진행될 것임을 추측할 수 있다.
<br>
2. Unsupervised Learning(비지도학습) : 타겟(답, label)이 없다.
 - Clustering(군집, 차원축소)


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
