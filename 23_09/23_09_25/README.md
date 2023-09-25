# Logistic Regression
1. 이진(Binary)분류 : 0과 1, Y/N와 같이 두 가지의 가능성만 존재함
2. 다중(Categorical)분류 : 세 가지 이상으로 분류할 수 있다.

## sigmoid 함수 <br>
  ![sigmoid](https://wikimedia.org/api/rest_v1/media/math/render/svg/9537e778e229470d85a68ee0b099c08298a1a3f6)
  ![sigmoid2](https://upload.wikimedia.org/wikipedia/commons/thumb/8/88/Logistic-curve.svg/640px-Logistic-curve.svg.png)
<br><br>

## Model Validation(평가)
<table style="text-align:center">
    <tr>
        <td></td>
        <td></td>
        <td colspan=2>분류결과</td>
    </tr>
    <tr>
        <td></td>
        <td></td>
        <td>Positive</td>
        <td>Negative</td>
    </tr>
    <tr>
        <td rowspan=2>실제</td>
        <td>Positive</td>
        <td style="background-color:yellow; color:black">True Positive(TP)</td>
        <td style="background-color:red; color:black">False Negative(FN)</td>
    </tr>
    <tr>
        <td>Negative</td>
        <td style="background-color:red; color:black">False Positive(FP)</td>
        <td style="background-color:yellow; color:black">True Negative(TN)</td>
    </tr>
</table>

  1. Accuracy(정확도) = (TP + TN) / (TP + TN + FP + FN)
       
  2. Precision(정밀도) = TP / (TP + FP)
   
  3. Recall(재현율) = TP / (TP + FN)

  4. F1-Score(조화 평균) = 2 / (1/Precision + 1/Recall) = 2 * (Precision * Recall) / (Precision + Recall)
<br><br>

## Cross Entropy Error(학습)
- 서로 다른 사건의 확률을 곱하여 엔트로피를 계산
- y : 실제값, y_hat : 예측값
1. Entropy(불확실성 척도) : 불확실성이 낮으면 분류 정확도가 낮아짐.

<br><br>

# Decision Tree &rarr; 나무형 모델
- 가능한 대답이 두 가지인 이진 질의 규칙을 바탕으로 최상위 루트 노드 질의 결과에 따라 가지를 타고 이동하면서 최종적으로 분류(문자) 또는 예측(숫자)을 나타내는 리프까지 도달
- Root Node : 최상위 노드
  - splitting : 하위 노드로 분리되는 것
  - branch : 노드들의 연결
- Decision Node : 2개의 하위 노드로 분리되는 노드
  - Parent Node : 분리가 발생하는 노드
- Leaf(Terminal Node) : 더 이상 분리되지 않는 최하위 노드 ~ 엔트로피가 0에 가깝다.
  - Child Node : 분리가 발생한 후 하위 노드

- 과적합(Overfitting) 문제
  - 각 노드는 동질성이 높고 불순도가 낮은 방향으로 분리한다. 그런데 너무 크고 복잡한 의사결정나무 모델을 생성하면 과적합 문제 발생한다.
  - '가지치기'방법을 이용해서 모델 성능 향상 및 과적합 예방.

- 나무형 모델에는 Hyperparameter가 많다. Hyperparameter는 학습자에 의해서 변경가능 하고 성능에 영향을 준다.