# 마크다운 실습

## 1. 문법
*[참고 : markdown cheatsheet](https://www.markdownguide.org/cheat-sheet/)*

### 1. Heading(제목)
- `#` : h1
- `##` : h2
- `###` : h3 

<br>

### 2. 목록
목록은 `-`를 사용하면 된다.
1. Unordered List
```md
- 목록1
- 목록2
    - 목록 2-1
    - 목록 2-2
```

2. Ordered List
```md
1. 목록1
2. 목록2
    1. 목록 2-1
    2. 목록 2-2
```
참고
```
- [x] todo list1
- [ ] todo list2
- [ ] todo list3
```
결과
- [x] todo list1
- [ ] todo list2
- [ ] todo list3

<br>

### 3. 코드 블록
```md
` `를 사용한다. 하나만 있다면 single

    ```python(사용하려는 language 작성, ex. html, python 등)
    print(f'hello world!')
    ```
이런식으로 사용하면 큰 규모의 코드를 작성할 수 있다.
```

<br>

### 4. Link
링크의 경우는 다음과 같이 작성하면 된다.
```md
[title](link주소)

example)
[google](https://google.com)
```

<br>

### 5. Image
마크다운을 작성하는 해당 폴더 내에 이미지가 있는 경우 다음과 같이 작성하면 된다.
```
![text](./image1.jpg)
```
결과

![사과](./1_google.jpg)

<br>

### 6. 텍스트
```
*텍스트* : Italic
**텍스트** : Bold
~~텍스트~~ : 취소선
```
결과

*안녕하세요*
**안녕하세요**
~~안녕하세요~~

<br>

### 7. 인용문
```
> 인용문
```
결과
> 안녕하세요

<br>

### 8. Horizontal Rule
`---`

결과
---

<br>

### 9. table(표)
```
|syntax|Description|
|--|--|
|Header|Title|
|Paragraph|Text|
```
결과
|이름|나이|
|--|--|
|홍길동|60|

<br>

---

*적용해보기*

# 1. 데이터 이해
## 1) 데이터의 이해
### i) 데이터와 정보
- 데이터의 특성
  
|구분|특성|
|--|--|
|존재적특성|객관적 사실(Fact, Raw Material)|
|당위적특성|추측, 예측, 전망, 추정을 위한 근거|

1. 정형데이터 : 정형화된 틀이 있고 연산이 가능하다
    - csv
    - 엑셀의 스프레드시트
    - 관계형 데이터베이스
2. 비정형 데이터 : 정형화된 틀이 없고 연산이 불가능하다
    - 소셜데이터
    - 댓글
3. 반정형 데이터 : 정형화된 틀이 있지만 연산은 불가능하다
    - xml
    - json
    - 로그데이터
