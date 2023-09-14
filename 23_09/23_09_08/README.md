[참고](https://github.com/Imshyeon/DesignPattern) <br>
    - b_coffeemanager <br>
    - b_coffeemanager_oop_singleton <br>
    - c_coffeemanager_poly <br>
    - d_coffeemanager_deco
    
<br>

1. 기능확장
    1. 주문 금액이 10000원 이상인 주문은 10% 할인하는 정책을 추가.

    2. 특정 계절에만 판매할 수 있는 계절음료 추가
        - 계절음료는 해당 음료의 판매기간이 아니라면 '해당음료는 계절상품입니다'를 출력 후 주문 취소.

    3. 자바칩,간얼음,휘핑크림,샷을 커피에 추가하는 기능을 구현해보자.
        ```python
        #  초코칩, 샷 추가 시 추가해야 할 클래스는 5개
                        Coffee
        SeasonCoffee            ChocoCoffee  ShotCoffee
        ChocoSeasonCoffee           ShotChocoCoffee
        ShotSeasonCoffee
        ``` 

        추가적으로 만들어야하는 클래스가 너무 많다 -> 비효율적 => Decoration Pattern

        <br>

## Decoration Pattern
- 주어진 상황 및 용도에 따라 어떤 객체에 책임을 덧붙이는 패턴


## 좋은 코드란
1. 실행 중에 제대로 동작하는 것
    - 모듈의 존재 이유
2. 변경을 위해 존재하는 것
    - 간단한 작업만으로 변경이 가능해야 한다.
3. 코드를 읽는 사람과 의사소통 하는 것


## 객체지향 SOLID 원칙
1. S(SRP) : 한 클래스는 하나의 책임만 가져야한다.
2. O(OCP) : 확장에는 열려있으나, 변경에는 닫혀있어야 한다.
3. L(LSP) : 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다. -> 호출부에서 기대하는대로 동작하도록 메서드를 오버라이딩 해야한다. (다형성)
4. I(ISP) : 특정 클라이언트를 위한 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.
5. D(DIP) : 추상화에 의존한다. 구체화에 의존하면 안된다.