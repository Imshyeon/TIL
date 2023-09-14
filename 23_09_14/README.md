# Numpy
1. 특징
  - 수학 및 과학적 연산을 쉽고 빠르게 지원한다.
  - 다차원 행렬을 효과적으로 처리한다.
  - 일반적으로 같은 데이터 타입(연속형 &rarr; 숫자데이터) 값을 구성된다.


## 1. 행렬
![img](https://hkilter.com/images/7/7a/Tensors.png)

1. Scalar - 0D Array - Rank0 Tensor
    ```
        a0 = np.array(9)
    ```
2. Vector - 1D Array - Rank1 Tensor
    ```
        a1 = np.array([1, 3, 5, 7, 9])
    ```
3. Matrix - 2D Array - Rank2 Tensor
    ```
        a2 = np.array([[1, 2, 3],
                       [4, 5, 6],
                       [7, 8, 9]])
    ```
4. Array - 3D Array - Rank3 Tensor
    ```
       a3 = np.array([[[1, 2],
                       [3, 4]],
                       [[5, 6],
                       [7, 8]],
                       [[9, 10],
                       [11, 12]]])
    ```
    - a[축, 행, 열] 순이다. 

<br>

## 2. shape, reshape, size, ndim, flatten
1. 만약 `array.shape` = (12,)이면 &rarr; 1차원의 Array이고 벡터 형태이다.

2. reshape(행,열)
   - `array.shape` = (3,4) &rarr; 3행 4열이고 ndim = 2이다.
   - ``.reshape(-1,1)` : 열은 지정했는데, 행 = -1 이면 '열의 값에 행을 맞춘다.' 라는 의미이다.

3. `.size` : 행렬의 요소의 개수
4. `.ndim` : 행렬의 차원
5. `.flatten` : 어떤 shape이던지 1차원으로 쭉 핀다.

<br>

## 3. 범위지정
1. `numpy.arange(n)` : 연속된 n개의 값 생성. for문의 range와 같다.

## 4. 특별한 형태의 Array 생성
1. `numpy.zeros` : 0으로만 구성
2. `numpy.ones` : 1로만 구성
3. `numpy.eye` = 3x3 단위행렬
4. 난수행렬
 - `numpy.random.rand` : 실수 난수
 - `numpy.random.randint` : 정수 범위의 난수 &rarr; 복원추출 형태로 동작(뽑은 것도 중복되어 또 뽑힐 수 있다)
   - `np.random.choice(np.arange(1, 46), size = (5 ,6), replace = False)` : replace = 복원 x
 - `numpy.random.seed` : 의사난수(Pseudo Random Number, 가짜 난수) 생성 초기값 지정 &rarr; 항상 같은 형태로 랜덤값을 만듦
 - `numpy.random.suffle` : 원소 섞기

## 5. Array 연산
1. 기본 연산 : 각각의 행과 열의 값을 매칭해서 산술 연산을 수행한다. 
2. 통계량 연산 : sum, mean, var(분산), std(표준편차), min, max, 중앙값, 최빈값, 범위
 - `min()` : 전체의 최소값
 - `min(axis=0)` : 각 열의 최소값 // axis=0 아래쪽 방향(행의 방향)으로 연산해라.. 라는 의미 &rarr; 파란색 화살표가 행의 방향
 - `min(axis=1)` : 각 행의 최소값 // axis=1 열의 방향으로 연산해라 &rarr; 초록색 화살표가 열의 방향
  
    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4d/Matrix_ko.svg/440px-Matrix_ko.svg.png" width="200">

 - `cumsum` : 누적합
 - `cumprod` : 누적곱

## Matrix 연산
### 행렬 곱

<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/9196c0c24ad20c3b18582bc78785fa405d91c7c3">
<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/17584944fc26dc38354b452ffcc64aa158cf8349">

- `M1.dot(M2)` : M1 @ M2
- `numpy.dot(M2,M1)` : M2 @ M1

### 전치 행렬
![위키백과_전치행렬](https://upload.wikimedia.org/wikipedia/commons/e/e4/Matrix_transpose.gif)

- `numpy.transpose(M1)` : M1의 전치행렬
- `M2.transpose()` : M2의 전치행렬 == M2.T