# 인공지능의 이해
1. Data : 과거 행동의 결과들
- 특징
  1. 복수형 -> 여러 개이다. | datum 단수형
  2. **만들어 지는 것**이다. 즉, 행동의 결과. 행동의 결과로 기록되면 '객관적 사실'이라고 한다.
  3. 기본적으로 과거형이다.

2. Analytics : 특징을 확인하는 일 -> Staticstics(통계)
- 특징
  1.  중심화 경향치(공통)
      1. 평균(mean)
      2. 중앙값
      3. 최빈값 
  2. 산포도(차이)
      1. 분산(var) : 평균에서 평균적으로 떨어져있는 정도
      2. 표준편차(std) : 루트(분산) 
      3. 범위(range)
      4. 최솟값(min)
      5. 최댓값(max)    

---

1. Business Intelligence(BI) <br>
Business Activities(행동의 결과로 Data 생성) <br>
-> 일부의 데이터를 수집, 저장 <br>
-> DataBase(DB) : CRUD <br>
-> Data Warehouse(DW) <br>
-> Data Mining(DM) <br>
-> **Decision Making(미래 행동에 영향 : 미래 예측)** <br>

결국, AI는 의사결정의 자동화를 지원하겠다는 의미이다.

---
<br>


<table style="text-align:center">
<thead>
  <tr>
    <td>Data Type</td>
    <td>통계 변수</td>
    <td>적용가능연산</td>
    <td>예시</td>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">문자</td>
    <td>명목형</td>
    <td>==, !=</td>
    <td>성별, 혈액형</td>
  </tr>
  <tr>
    <td>순서형</td>
    <td>위의 연산자, >, <, >=, <=</td>
    <td>메달</td>
  </tr>
  <tr>
    <td rowspan="2">숫자</td>
    <td>이산형(등간변수)</td>
    <td>위의 연산자, +, -</td>
    <td>0이 의미를 가지지 않음. <br> ex. 온도, 인덱스</td>
  </tr>
  <tr>
    <td>연속형(비율변수)</td>
    <td>위의 연산자, +, -, *, /</td>
    <td>0이 의미를 가짐. <br> ex. 무게, 속도, 돈,,</td>
  </tr>
</tbody>
</table>

* 과학적인 척도는 연속형이라고 할 수 있다.
* 숫자는 산술연산, 비교연산이 가능하지만 문자는 산술연산은 안되고 비교연산은 (==, !=)이 가능하다. -> 의미가 있다!
  

---

1. Data Structure : Data가 모여있는 모양
- Vector
- Table
- Tree
- Network
- ,,,
