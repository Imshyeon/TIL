# Data Structure
* 문자열 - Structured
* 리스트 - Structured
* 튜플 - Structured
* 딕셔너리 - Unstructured
* casting

---

1. Big Data
- Volume(크기) : *bit(0/1) => binary digit / digit(0-9)*
  - 32bit &rarr; 2^32 = 4GB .. address를 pointing 할 수 있는 최대 수가 4GB.
  - 64bit &rarr; 2^64 = 16EB
    <br>
    <img width="300" src="https://cryptosmith.files.wordpress.com/2020/12/memory-sizes-to-yotta.png">
    <br>

  - **Big Data는 상대적인 개념**이다. 만약 내가 32bit 컴퓨터인데, 8GB를 받고싶다.. 하지만 받을 수 없음 &rarr; 8GB는 Big Data

- Variety(다양성)
  - Structured(정형) : Data type이나 Size가 정해져 있다. &raquo; RDB(SQL)
  - Unstructured(비정형) : Data type이나 Size가 사전에 정해지지 않아도 처리한다. &rarr; 이미지, 자연어 &raquo; NoSQL(Not Only SQL)

- Velocity(속도)
  - 생성되는 속도가 매우 빠름
  - 의미를 가지는 시간이 짧아짐

---

1. Structured : Index
2. Unstructured : Index가 없다.
3. Casting : 데이터 타입이나 구조를 변경하는 것.

<br>
<br>

# Function and Module
1. 함수는 Processor, Memory(RAM), Disk(SSD) 중에서 기본적으로 Memory, Disk에 있다.
  - python이 실행(execute)이 되면서 Disk에서 Memory로 올라와있을 것이다.
  - 함수는 메모리에 올라와 있어야 실행 가능하다.

2. 모듈은 기본적으로 Disk에 File로 존재한다.
  - 이 모듈을 사용하기 위해선 메모리에 올라갈 필요가 있다.

<br>
<br>

# Class and Package
1. Class : 개발자에 의해 지정된 독립된 메모리 공간(구조)이다. &rarr; 기본적으로 메모리 내에 할당된다.
   - 함수와 변수를 하나의 객체로 묶어서 관리한다.
   - 선언된 Class 사용을 위해 인스턴스 생성이 필요하다. &rarr; ex. instance = Class() 
   - 인스턴스 간에서는 독립된 메모리 구조를 사용한다.
   - Class도 결국은 함수를 사용하기 위한 방법이다.
- Class Method : Class 내에 선언된 함수
- Class Member : Class 내에 선언된 변수
  - Instance Member : Class 내 함수에 선언된 변수, instance를 생성한 다음에 접근이 가능한 변수

2. Package : 관련된 모듈을 디렉토리 구조를 사용하여 계층적으로 관리한다.
   - import나 from ~ import ~ 로 불러와서 사용한다. 