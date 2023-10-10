# TensorFlow
1. 데이터 흐름 프로그래밍을 위한 Open Source Software Library
2. Neural Network 같은 Machine Learning Modeling에 활용
3. 특징
   1. Keras API 활용
   2. 플랫폼 관계 없이 모델을 학습시키고 배포 가능
   3. 빠른 프로토 타입 제작과 디버깅 구현 가능

## 1. Keras
1. Python 기반의 Deep Learning Framework
2. 사용자는 복잡한 내부 엔진에 대해서 알지 않아도 됨
3. 직관적인 API를 통하여 MLP, CNN, RNN 등의 모델 생성 가능
4. 다중 입력 및 다중 출력 구성 가능

- GPU : 단순 대량 연산에 적합 &rarr; Keras 사용할 때 GPU 써야한다!!

## 2. Tensor
1. Neural Network 학습의 기본 데이터 단위
   - 숫자 데이터를 담기 위한 컨테이너
   - 임의의 차원 또는 축(Rank)을 가짐

2. Tensor in NLP(Natural Language Processing)
   - 문장과 단어를 숫자 벡터로 매핑함. Vector(단어 하나) 자체가 Rank 1
   - 만약 문장을 구성하면 Rank 2
   - 여러 개의 문장 &rarr; Rank 3(mini-batch input)

3. Keras Modeling
   1. Defind(모델 신경망 구조 정의)
   2. Compile(모델 학습방법 설정)
   3. Fit(모델 학습 수행)
   4. Evaluate(모델 평가)
   5. Predict(모델 적용)
   6. 목표 달성 시 까지 반복
