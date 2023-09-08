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

