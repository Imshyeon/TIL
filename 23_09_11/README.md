* dbbrowser 설치

    **homebrew** : `brew install --cask db-browser-for-sqlite`

<br>

# Template Method Pattern
1. Template Method Pattern : 알고리즘의 구조를 메소드에 정의하고, 하위 클래스에서 알고리즘 구조의 변경없이 알고리즘을 재정의하는 패턴
    ![img](https://upload.wikimedia.org/wikipedia/commons/2/2a/W3sDesign_Template_Method_Design_Pattern_UML.jpg)

2. [e_template_method](https://github.com/Imshyeon/DesignPattern/tree/main/e_template_method) => oop(다형성을 이용한 유연성 확보)적으로 문제가 발생 
- library : 작성한 코드
  - DAO.py
  - AbstractDAO.py
- client : 클라이언트 입장에서 실행
  - DAO.py => **구현체**, 우리가 만든 추상클래스를 상속받도록 강요
- main.py

<br>

# Strategy Pattern
1. Strategy Pattern : 객체의 행위를 동적으로 바꾸고 싶은 경우 직접 행위를 수정하지 않고 전략을 바꿔 주기만 함으로서 행위를 유연하게 확장하는 방법

2. [f_strategy](https://github.com/Imshyeon/DesignPattern/tree/main/f_strategy) => 상속을 시키지 않고 사용자가 객체를 쓸 수 있도록 한다. 상속을 안쓰면 객체 간의 결합도가 낮아진다(Good!). 
- library
  - DAO.py => **구현체**, 생성자를 통해서 connection을 받도록 했다.
  - AbstractConnectionCreator.py
- client
  - ConnectionCreator.py => 커넥션을 하고 그것을 반환하는 것만 한다. 설계 외적인 클래스
- main.py

<br>

# Template Callback Pattern
1. Template Callback Pattern : Strategy Pattern의 변형으로 DI(Dependency Injection) 전략을 내부 클래스로 구현하여 매개변수로 전달하는 패턴

2. [g_template_callback](https://github.com/Imshyeon/DesignPattern/tree/main/g_template_callback)
- library
  - DAO.py
- main.py