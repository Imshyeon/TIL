# 알고리즘

1. 조건
    ```python
    # 세 수 중 최대값 구하기
    def max(a, b, c):
        max = a
        if(b > max): max = b
        if(c > max) : max = c
        return max

    # 세 수 중 최소값 구하기
    def min(a, b, c):
        min = a
        if(b < min) : min = b
        if(c < min) : min = c
        return min
    
    # 세 수 중 중간값 구하기
    def med(a, b, c):
        if(a >= b):
            if(b >= c) : return b
            if(a <= c) : return a
        elif(a > c) : return a
        elif(b > c) : return c
        else: return b

    print('max:',max(50,255,30))
    print('min:',min(50,255,30))
    print('med:',med(50,255,30))    

    # 결과 : max: 255
    #        min: 30
    #        med: 50
    ```

<br>

2. 반복
    ```python
    # 1 + 2 + 3+ .. + n = sum
    # 매개변수로 n을 입력받아 위와같은 형태로 출력하시오
    def q1(n):
        st='1'
        sum=1
        
        for i in range(2,n+1):
            st += '+' + str(i)
            sum += i
        st += '=' + str(sum)
        return st
                
    print(q1(10))

    # 결과 : 1+2+3+4+5+6+7+8+9+10=55

    ```

    ```python
    # 다이아몬드 별찍기
    # 사용자로 부터 2이상의 자연수를 입력 받아
    # 한 변의 길이가 사용자의 입력값인 다이아몬드를 그려보시오
    #     *      
    #    ***    
    #   *****    
    #  *******  
    # *********   
    #  *******   
    #   *****   
    #    ***    
    #     *   
    
    # 1. 문제 -- 공백까지 해서 만들어보자..
    def q2(n):
        st='*'
        blank=' '
        for i in range(1,n+1):
            print(blank*(2*n-i),st*(i-1)+st*i)
        for j in range(n-1,0,-1):
            print(blank*(2*n-j),st*(j-1)+st*j)
        
    print('==')
    q2(5)

    '''
    결과 : 공백이 적용되지 않음.
    ==
          *
         ***
        *****
       *******
      *********
       *******
        *****
         ***
          *
    '''

    # 2. 답
    # *의 개수는 홀수로 증가 : 2n-1
    # 공백의 개수 : cnt-n
    # n은 1부터 1씩 증가하는 자연수
    # cnt는 입력값
    # ---------
    # *의 개수는 홀수로 감소 : 2n-1
    # 공백의 개수는 1부터 1씩 증가
    # n은 cnt-1부터 1씩 감소하는 자연수

    def print_diamon(cnt):
        print('=====')
        for i in range(cnt):
            n=i+1
            for j in range(cnt-n):
                print(' ', end='')
            for k in range(2*n-1):
                print('*',end='')
            print()
            
        white_space=1
        for i in range(cnt-1,-1,-1): 
            for j in range(white_space):
                print(' ',end='')
            for k in range(2*i-1):
                print('*',end='')
            white_space += 1
            print()
        

    print_diamon(5)
    '''
    결과 : 공백이 적용됨.
    =====
        *
       ***
      *****
     *******
    *********
     *******
      *****
       ***
        *
    '''
    ```

<br>


3. math
- Q1. 매개변수로 전달받은 숫자가 소수인지 아닌지 판별
    - 소수 : 1과 자기 자신만으로 나누어 떨어지는 1보다 큰 양의 정수.

        ![img](https://dbscthumb-phinf.pstatic.net/2765_000_373/20210318063335630_PHXLVN4C7.gif/94197_1.gif?type=m1500&wm=N)
    
    - 소수의 정의에 따라서 코딩
    ```python
    def is_prime(num):  # 내가 푼 부분
        if num == 2 : return True
        for x in range(2,num):
            if num%x == 0:
                return False
        return True

    def is_prime_ans(num):
        # if num==2 : return True   # 1.
        if num % 2 == 0 and num != 2 : return   # 2. 
        
        # for i in range(3,num):  # 1. range(2,num)하고 위에 if를 없애도 되긴 함.. but 그래도 적어주자
        #     if num%i==0:
        #         return False
        # return True

        for i in range(3,num,2):  # 2. range(2,num)하고 위에 if를 없애도 되긴 함.. but 그래도 적어주자
            if num%i==0:
                return False
        return True

    #------
    # test.py
    import unittest
    import sys
    sys.path.append(r'C:\Users\KSH\Desktop\CODE\Algorythm\a_basic')
    from c_math import *
    from math import *
    import random

    class TestBasic(unittest.TestCase):
        def test_is_prime(self):
            self.assertTrue(is_prime(18))    # 나 => 소수가 아니니까 False로 오류
            self.assertTrue(is_prime_ans(7))    # 답1 => 소수니까 True로 ok
    ```
    <br>

    - 소수가 아닌 수를 생각해서 코딩(제곱근 이용)
  
    >예시) 12 = 1 x 12 <br> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;&nbsp; 2 x 6 <br> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;&nbsp;&nbsp;3 x 4<br> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;&nbsp;&nbsp;4 x 3<br> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;&nbsp;&nbsp;6 x 2<br> &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;&nbsp;12 x 1
    
    이처럼 12는 가운데를 기준으로 대칭 구조를 갖는다.

    ```python
    from math import sqrt
    '''
    소수가 아닌 수를 생각해보자
    4라는 숫자를 예를 들어보면 4는 1x4 , 2x2, 4x1로 소수가 아니다.
    sqrt(4) = 2 이다.
    그렇다면 for i in range(sqrt(num)+1)의 의미는 다음과 같다. : 0~3까지 for문을 반복하는데, 그 사이에 있는 i를 이용해 num을 나눴을 때 나머지가 0이라면 num은 소수가 아니다.
    즉, sqrt를 쓴 이유는 반복의 횟수를 줄이기 위함이다.
    '''
    def is_prime_plus(num):
        for i in range(2,int(sqrt(num)+1)):
            if num % i == 0:
                return False
        return True

    #------
    # test.py
    import unittest
    import sys
    sys.path.append(r'C:\Users\KSH\Desktop\CODE\Algorythm\a_basic')
    from c_math import *
    from math import *
    import random

    class TestBasic(unittest.TestCase):
        def test_is_prime2(self):
            self.assertTrue(is_prime_plus(7))
    ```
    <br>
- Q2. 2부터 매개변수로 입력받은 값 사이에 존재하는 소수를 구해 리스트로 반환하는 함수를 작성
    ```python
    def prime_numbers(num):
    prime_list=[]
    for i in range(2,num):
        if is_prime_plus(i):
            prime_list.append(i)
        
    return prime_list
    ```
<br>

- Q3.최대공약수
    ```python
    def gcd1(a, b):
    if a > b : min = b
    min = a
    gcd=1
    # for i in range(1,min+1):
    #     if a % i == 0 and b % i == 0 :
    #         gcd *= i
    # return gcd

    for i in range(min,0,-1):
        if a % i == 0 and b 

    # 유클리드 호제법을 활용한 최대공약수 구하기
    # a, b 두 수가 있을 때(a>b)
    # a를 b로 나눈 나머지는 두 수의 최대 공약수의 배수이다.
    def gcd2(a, b): 
        while b > 0 :
            a, b = b, a % b        
        return a    
    ```
<br>

 - Q4. 최소공배수
 ```python
def lcm1(a, b):
    gcdValue = gcd2(a,b)
    # a * b / gcdVal와 같은 의미이다!
    return gcdValue * (a / gcdValue) * (b / gcdValue)
 ``` 
<br>

- Q5. 팩토리얼
```python
def factorial1(num):
    if num < 0 : return -1
    res = 1
    for i in range(1, num+1):
        res *= i
    return res

def factorial_recursive(n): #재귀함수 사용 -> 그렇지만 파이썬에선 불추..
    if n == 0 or n == 1:
        return 1
    return n * factorial_recursive(n-1)

def factorial_tail(n, result=1) : # 꼬리재귀함수
    if n == 0:-
        return result
    else:
        return factorial_tail(n-1,n*result)

```
<br>

- Q6. 피보나치 수열
    - 피보나치 수열 : 첫째 및 둘째 항이 1이며 그 뒤의 모든 항은 바로 앞 두 항의 합인 수열이다
        
        ![img](https://upload.wikimedia.org/wikipedia/commons/8/83/FibonacciBlocks.png)

    ```python
    def fibonacci(num):
    if num < 1: return -1
    prev, cur = 1, 1
    for i in range(3,num+1):
        prev, cur = cur, prev+cur
    return cur

    # 피보나치 수열 재귀함수 이용. 이렇게 재귀함수를 쓰면 안된다!
    def fibo_recursive(n):
    if n == 0:
        return 0
    elif n == 1 or n == 2 :
        return 1
    else:
        return fibo_recursive(n-1) + fibo_recursive(n-2)
    
    def fibo_tail(n, before=0, next=1):
        if n == 0:
            return 0
        elif n == 1:
            return next
        else:
            return fibo_tail(n-1, next, before+next)
    ```


<br>

# Linked List : 전통적인 방식의 List와 비교하여 공부
1. LinkedList의 메모리 구조 : 찾을 때(Read)는 시간 복잡도가 O(0)이 된다.

2. LinkedList의 삭제 과정 : 기존의 전통적인 방식에서는 O(n)만큼의 시간이 걸린다. 하지만 LinkedList는 그냥 참조를 끊어버리면 된다. => garbage collector : 더이상 해당 객체를 참조하고 있는 변수가 없으면, 메모리에서 삭제해버림. 자연스럽게 삭제된다.

* duck typing?

# Hash Table 
1. Hash : 임의의 길이의 데이터를 수학적 연산을 통해 고정된 길이의 데이터로 매핑하는 함수
2. Hash Table : 해시 함수로 얻은 해시를 키로 활용하여 index로 사용하고 해당 index에 데이터를 저장
    - 장점 : 검색이 빠르다
3. Hash 충돌 : 다른 key가 동일한 hash 값을 갖는 현상
    - 해결방법
        - Chaining : 중복 해시 값이 있는 경우 Linked List를 활용해 데이터를 저장
        - Open Addressing : 충돌 발생 시 해시값이 아닌 다른 곳에 데이터 저장


* list 컴프리핸션?
* client, callback - template?