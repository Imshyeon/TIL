# Data Processing
## 1. 결측치
- 전체 데이터의 특징을 확인할 수 없게 만든다.
- 표현방법
  - NA(na)
  - NaN
  - Null
  - '' (공백)
  
<br>

- 결측치 확인
  1. `.value_counts(dropna=False)` : 결측치를 포함하여 빈도분석 결과 출력 | dropna=True가 default임을 알고있자
  2. `.isnull()` : 결측치를 True로 출력
     - `.isnull.sum(axis=0)` : 각 열(Column)별로 결측치 개수 확인 | python은 True+True=2 처럼 bool타입을 연산할 수 있음을 이용
     - `.isnull.sum(axis=1)` : 각 행(Row)별로 결측치 개수 확인
  3. `.notnull()` : 결측치를 False로 출력


    - 결측치 막대 그래프
        ```python
        import missingno as msno

        msno.bar(TD,
                figsize = (15, 7),
                color = (0.2, 0.2, 0.8))    # RGB를 퍼센트로 줌
        ```
        ![Alt text](image.png)

    <br>

    - 결측치 Matrix : 결측치가 어디에 위치해 있는지 보여줌. 하얀 부분이 결측치
        ```python
        msno.matrix(TD,
                figsize = (15, 7),
                color = (0.8, 0.2, 0.2))
        ```
        ![Alt text](image-1.png)

<br>

- 결측치 삭제 : 열 삭제 또는 행 삭제
  - `.dropna(thresh=n, axis=1)` : n개 이하 측정값(Non-Null)이 있는 열 삭제
  - `.dropna(subset=['age'], how='any', axis=0)` : age행을 기준으로 결측치가 있는 행 삭제
    - how = 'any' : 기본값  &rarr; 행 또는 열에서 하나 이상의 결측치가 있는 경우 해당 행 또는 열이 삭제된다. 즉, 결측치가 하나라도 있으면 해당 행/열이 삭제
    - how = 'all' : 행/열에서 모든 값이 결측치인 경우에만 해당 행/열이 삭제.

<br>

- 결측치 치환 (숫자, 문자)
  - `.fillna(int(DF['age'].mean(axis=0)), inplace = True)` : 연속형 데이터 치환, 결측치를 평균값으로 치환 [숫자]
  - `.fillna(most_freq,inplace = True)` : 명목형 데이터 치환, 결측치를 최빈값으로 치환 [문자]
    ```python
    most_freq = TD['embark_town'].value_counts(dropna = True).idxmax() # 'Southampton'리턴. Southamton이 인덱스값
    TD['embark_town'].fillna(most_freq, inplace = True)
    ```
  - `.fillna(method='ffill', inplace = True)` : 이전 데이터포인트로 치환
  - `.fillna(method='bfill', inplace = True)` : 다음 데이터포인터로 치환

<br>

## 2. Filtering
- 나이가 10살 이상이면서 20살 미만 
    ```python
    Filter_1 = (TD.age >= 10) & (TD.age < 20)

    D.loc[Filter_1, :].head()
    ``` 
<br>

## 3. 데이터프레임 합치기
- `.concat()` : 연결시키는 느낌
  ```python
  pd.concat([TB1, TB2], axis = 0)   # 행의 방향으로 테이블 합침
  ```
  ![Alt text](image-2.png)

    <br>

  ```python
  pd.concat([TB1, TB3], axis = 0, ignore_index = True)  # ignore_index = True : 라벨 새로 구성
  ```
  ![Alt text](image-4.png)
  
    <br>

  ```python
  pd.concat([TB1, TB2], axis = 1)
  ```
  ![Alt text](image-5.png)
  
<br>

- `merge()`
  ```python
  pd.merge(TB1, TB2, on = ['Name', 'Gender'])
  ```
  ![Alt text](image-3.png)
  
<br>

## 4. 그룹연산
- `groupby()`
  ```python
  grouped = TD.groupby(['class']) # class를 기준으로 DataFrameGroupBy 객체 생성 -> 1등실, 2등실, 3등실
  grouped   # <pandas.core.groupby.generic.DataFrameGroupBy object at 0x7ad8526826b0>
  grouped.get_group('First').head(3)
  ```
  ![Alt text](image-6.png)

  <br>

  ```python
  for key in ['First', 'Second', 'Third']:
  print(grouped.get_group(key).head(3))
  print('\n')
  ```
  ![Alt text](image-7.png)

  <br>

- `groupby()` - 'class' & 'sex' 기준
  ```python
  grouped_TWO = TD.groupby(['class', 'sex'])
  grouped_TWO.get_group(('First', 'female')).head(3)

  for key, group in grouped_TWO:
  print('* key :', key)
  print('* number :', len(group))
  print(group.head(3))
  print('\n')
  ```

  ![Alt text](image-8.png)
  ```shell
  * key : ('First', 'female')
  * number : 94
       age     sex  class     fare  survived
  1   38.0  female  First  71.2833         1
  3   35.0  female  First  53.1000         1
  11  58.0  female  First  26.5500         1


  * key : ('First', 'male')
  * number : 122
       age   sex  class      fare  survived
  6   54.0  male  First   51.8625         0
  23  28.0  male  First   35.5000         1
  27  19.0  male  First  263.0000         0


  * key : ('Second', 'female')
  * number : 76
       age     sex   class     fare  survived
  9   14.0  female  Second  30.0708         1
  15  55.0  female  Second  16.0000         1
  41  27.0  female  Second  21.0000         0


  * key : ('Second', 'male')
  * number : 108
       age   sex   class  fare  survived
  17   NaN  male  Second  13.0         1
  20  35.0  male  Second  26.0         0
  21  34.0  male  Second  13.0         1


  * key : ('Third', 'female')
  * number : 144
       age     sex  class     fare  survived
  2   26.0  female  Third   7.9250         1
  8   27.0  female  Third  11.1333         1
  10   4.0  female  Third  16.7000         1


  * key : ('Third', 'male')
  * number : 347
      age   sex  class    fare  survived
  0  22.0  male  Third  7.2500         0
  4  35.0  male  Third  8.0500         0
  5   NaN  male  Third  8.4583         0
  ```
  
  <br>

- `agg()`
  ```python
  grouped_TWO.agg(['mean', 'std'])  # 멀티 인덱스 : 인덱스가 class, sex이다.
  ```
  ![Alt text](image-9.png)
 
  <br>

  ```python
  grouped.agg({'fare' : ['min', 'max'], 'age' : ['mean', 'std']})   # fare, age열에 각각 다른 함수 적용
  ```
  ![Alt text](image-10.png)

  <br>

- `filter()`  
  ```python
  grouped.filter(lambda x : len(x) >= 200).head()   # 데이터 개수가 200개 이상인 그룹의 결과만 필터링
  grouped.apply(len)
  ```
  ![Alt text](image-11.png)
  ```shell
    class
    First     216
    Second    184
    Third     491
    dtype: int64
  ```

  <br>

  ```python
  grouped.filter(lambda x: x.age.mean() < 30).tail()    # 나이의 평균이 30보다 작은 그룹의 결과만 필터링
  grouped.age.mean()
  ```
  ![Alt text](image-12.png)
  ```shell
    class
    First     38.233441
    Second    29.877630
    Third     25.140620
    Name: age, dtype: float64
  ```

<br>

## 5. pivot_table()
- 한 개의 적용함수
    ```python
    TD_1 = pd.pivot_table(TD,
                        index = 'class',   # 만들어지는 TD_1의 index 영역이 class가 됨
                        columns = 'sex',   # 만들어지는 TD_1의 열이 sex가 됨
                        values = 'age',    # TD_1의 값들은 age
                        aggfunc = 'mean')  # 값을 채울 때, 평균으로 채운다.

    TD_1
    ```
    ![Alt text](image-13.png)

    <br>

- 두 개의 적용함수
    ```python
    TD_2 = pd.pivot_table(TD,
                        index = 'class',
                        columns = 'sex',
                        values = 'survived',
                        aggfunc = ['mean', 'sum'])  # 평균 생존률, 생존자 수

    TD_2
    ```
    ![Alt text](image-14.png)

    <br>

- 다중 인덱스, 다중 데이터, 다중 함수
    ```python
    TD_3 = pd.pivot_table(TD,
                        index = ['class', 'sex'],
                        columns = 'survived',
                        values = ['age','fare'],
                        aggfunc = {'age' : ['mean', 'std'], 'fare' : ['min', 'max']})

    TD_3
    ```
    ![Alt text](image-15.png)

<br>

## 6. Multi-Index
`.xs()` : Cross Section
- 행 멀티인덱스
    ```python
    TD_3.index
    TD_3.xs('First', level = 'class', axis = 0) # class 중에서 First만 보겠다.
    ```

    ```shell
    MultiIndex([( 'First', 'female'),
                ( 'First',   'male'),
                ('Second', 'female'),
                ('Second',   'male'),
                ( 'Third', 'female'),
                ( 'Third',   'male')],
            names=['class', 'sex'])
    ```
    ![Alt text](image-16.png)

    <br>

    ```python
    TD_3.xs(('First', 'male'), level = ['class', 'sex'], axis = 0)
    ```
    ![Alt text](image-17.png)

- 열 멀티인덱스
    ```python
    TD_3.columns
    TD_3.columns.set_names(['Header', 'Fuction', 'Survived'], inplace = True)
    TD_3.columns.set_levels(['Dead', 'Alive'], level = 2, inplace = True)   # Survived의 level=2이고, 0이면 Dead로 1이면 Alive
    ```

    ```shell
    MultiIndex([( 'age', 'mean', 0),    # 사망자의 평균 나이
                ( 'age', 'mean', 1),    # 생존자의 평균 나이
                ( 'age',  'std', 0),
                ( 'age',  'std', 1),
                ('fare',  'max', 0),
                ('fare',  'max', 1),
                ('fare',  'min', 0),
                ('fare',  'min', 1)],
            names=[None, None, 'survived'])

    MultiIndex([( 'age', 'mean', 0),
                ( 'age', 'mean', 1),
                ( 'age',  'std', 0),
                ( 'age',  'std', 1),
                ('fare',  'max', 0),
                ('fare',  'max', 1),
                ('fare',  'min', 0),
                ('fare',  'min', 1)],
            names=['Header', 'Fuction', 'Survived'])

    MultiIndex([( 'age', 'mean',  'Dead'),
                ( 'age', 'mean', 'Alive'),
                ( 'age',  'std',  'Dead'),
                ( 'age',  'std', 'Alive'),
                ('fare',  'max',  'Dead'),
                ('fare',  'max', 'Alive'),
                ('fare',  'min',  'Dead'),
                ('fare',  'min', 'Alive')],
            names=['Header', 'Fuction', 'Survived'])
    ```
    ![Alt text](image-18.png)

    <br>

    ```python
    TD_3.xs('Alive', level = 'Survived', axis = 1)  # 생존자 정보
    ```
    ![Alt text](image-19.png)

<br>

## 7. etc
  - `.vaule_counts()`
  ```python
  TD[['sex', 'class']].value_counts() # pivot 돌려서 count값 얻은 것과 같음
  ```

  ```shell
  sex     class 
  male    Third     347
  female  Third     144
  male    First     122
          Second    108
  female  First      94
          Second     76
  dtype: int64
  ```

  <br>

  - `.nunique()` : 몇가지나 있나?
  ```python
  TD[['sex', 'class']].nunique()
  ```

  ```shell
  sex      2  # 성별은 2개
  class    3  # 클래스는 3개
  dtype: int64
  ```

  <br>

  - `.replace()`
  ```python
  TD['sex'] = TD['sex'].replace('male', 'MAN')
  TD.loc[TD['sex'] == 'MAN', :][:2]
  ```
  ![Alt text](image-20.png)

  <br>

  ```python
  TD[['class']] = TD[['class']].replace({'First':'1st', 'Second':'2nd', 'Third':'3rd'})
  TD.loc[[1, 9, 0], :]    # 1, 9, 0 번만 보자
  ```
  ![Alt text](image-21.png)

  <br>

  ```python
  import numpy as np

  TD[['age']] = TD[['age']].replace(np.nan, int(TD.age.mean()))   # 결측치 대체
  TD.loc[[5], :]
  ```
  ![Alt text](image-22.png)
