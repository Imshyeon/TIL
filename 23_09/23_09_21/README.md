# Machine Learning
## Model Validation
### Validation Approach
Testing Error가 Generalization Error와 가까울 것인가? &rarr; Validation Approach
1. Generalization Error
   - 학습된 예측 모델을 실무 데이터에 적용 시 발생하는 에러로 현실적으로 측정 불가능하다.
<br>

- Training Data를 Training Data, Validation Data로 분리.
- Validation Error로 최종 모델을 선택
- Testing Data에 최종 선택된 모델을 적용해 얻은 MSE &rarr; 실무 데이터에 대한 Generalization Error 추정에 Testing Error 사용.

```python
from sklearn.model_selection import train_test_split

X_remain, X_test, y_remain, y_test = train_test_split(Elec[['surface_area']],
                                                      Elec['electricity'],
                                                      test_size = int(len(Elec) * 0.2),
                                                      random_state = 2045)


X_train, X_valid, y_train, y_valid = train_test_split(X_remain, y_remain,
                                                      test_size = int(len(Elec) * 0.2),
                                                      random_state = 2045)

print(X_train.shape, y_train.shape) # (462, 1) (462,)
print(X_valid.shape, y_valid.shape) # (153, 1) (153,)
print(X_test.shape, y_test.shape)   # (153, 1) (153,)            
```
- Training Data : Validation Data : Testing Data = 6 : 2 : 2
<br><br>

## Regression Analysis (수치 예측)
- 과거 결과값을 기준으로 미래 결과값(수치)을 예측하는 방법 
1. 단일 회귀 분석 : Output에 영향을 주는 Input이 1개인 경우. &rarr; y_hat = wx + b
2. 다항 회귀 분석 : y_hat = w<sub>1</sub>x<sup>2</sup> + w<sub>2</sub>x + b
3. 다중 회귀 분석 : Input이 여러 개인 경우.(Output은 1개) &rarr; y_hat = w<sub>1</sub>x<sub>1</sub> + w<sub>2</sub>x<sub>2</sub> + b
