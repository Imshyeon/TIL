# Ensemble(앙상블)
- 앙상블 : 여러 모델을 적용해서 성능을 개선하는 방법
- 랜덤 포레스트 : 의사결정나무 앙상블
  - 다수의 의사결정나무 모델로부터 예측값 생성.
  - 모델 학습에 다양성과 임의성(Random)을 부여
  - 모델 성능을 향상시키고 과적합 발생 가능성을 감소
  - 올바른 예측은 **강화**하고, 잘못된 예측은 **상쇄**하는 경향 존재

1. 다양성 - 배깅
   - 주어진 data를 사용해서 여러개의 서로 다른 Train Data를 생성. &rarr; 생성된 Train Data 마다 별도의 의사결정나무 모델을 생성한다. Hyperparameter로 의사결정나무 개수 지정
   - 다양한 Train Data는 Bootstrap 방식으로 생성하는데, Bootstrap Data는 원래 데이터에서 단순 복원 임의 추출법으로 생성한다.

2. 임의성 - Random Subspace
   - 의사결정나무 생성 시 변수 무작위 선택
   - 원래 변수에서 무작위로 입력 변수를 추출하여 적용한다. 
   - Hyperparameter:max_features &rarr; 기본값 : sqrt(전체 변수 개수)

3. Cross Validation
   - Overfitting 방지를 위해서 수행. 
   - Validation 한번만 수행 시 특정 Data에만 최적화될 가능성이 있다 따라서 다양하게 Training Data와 Validation Data를 변경하면서 모델 평가를 진행한다.
   1. K-Fold Cross Validation
      - Training Data를 무작위로 균등하게 K개의 그룹으로 나눠서 검증
        - (K-1)개의 Training Data, 1개의 Validation Data
        - 보통 K는 5~10 정도로 선택
        - K개의 결과의 평균을 Validation Data에 적용해서 평가.
      - 데이터가 충분히 많으면 K-Fold를 사용하지만 데이터가 적다면 데이터의 개수만큼 교차검증을 수행한다(LOOCV)

4. Boosting
   - 모델 여러 개를 순차적으로 학습해서 최종 모델을 생성 &rarr; 단계를 거치면서 이전 단계 단점을 보완하며 더 좋은 모델을 학습한다.
     - AdaBoost, GBM &rarr; sklearn
     - XGBoost, LightGBM &rarr; 추가 패키치 설치 필요

   1. Adaptive Boosting(AdaBoost)
      - 각 학습 단계에서 새롱누 약한 분류기를 순차적으로 학습
      - 이전 학습 단계 약한 분류기의 단점을 보완하여 학습 진행한다. &rarr; 잘못 분류된 데이터의 가중치를 조정.
      - 이전 학습에서 틀린 데이터가 더 잘 뽑힐 수 있도록 가중치를 조정.

   2. Gradient Boosting Machine(GBM)
      - 각 학습 단계에서 새로운 약한 분류기를 순차적으로 학습
      - 이전 약한 분류기의 오차를 사용하여 학습. &rarr; 약한 분류기가 놓친 부분을 추가로 학습.
      - 학습이 진행되면서 오차가 점점 감소 &rarr; 학습된 약한 분류기를 조합하여 최종적으로 성능이 좋은 모델을 생성