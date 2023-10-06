# Deep Learning

## 1. Artificial Neural Network(인공신경망)
## Neural Network
1. 머신러닝 분야에서 연구되는 학습 알고리즘으로 수치예측, 범주예측, 패턴인식, 제어분야에 응용되고있다.
2. 인간의 뇌 구조를 모방해서 만들어졌다.

## Perceptron
1. 인공신경망의 한 종류(선형분리기)로 노드의 입력값과 가중치의 곱을 모두 합했다.
2. 합한 값이 활성화함수 임계치 이상이면 1, 미만이면 0을 출력한다.

## Multi-Layer Perceptron
모델의 capacity를 극대화하기 위해서 Multi-Layer Perceptron을 적용한다.

![img](https://ko.d2l.ai/_images/mlp.svg)
- 다층 퍼셉트론 : 퍼셉트론으로 해결할 수 없는 비선형 분리 문제에 필요하다.
- 여러 층의 퍼셉트론을 쌓아서 동작하고 Hidden Layer가 1개(1층)이다.

- DNN : Hidden Layer가 2개 이상이다. &rarr; 단순한 함수를 여러 개(다층)로 하여 예측.
    ![dnn](https://heung-bae-lee.github.io/image/Deep_Neural_Network.png)

    &rarr; depth가 커질수록 파라미터가 증가하고, 파라미터가 증가하면 학습속도에 부정적인 영향을 줄 수 있다


## Error Backpropagation(오차 역전파)
수치 미분을 수행하지 않고 학습에 필요한 편미분값을 획득 가능하세 해준다. &rarr; 수치 미분을 하지 않아서 예측 시간이 줄어듦.
- 원리
  1. 연쇄법칙(Chain Rule)
  2. 역전파(Backpropagation)