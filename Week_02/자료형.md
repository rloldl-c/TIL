# 프로그래밍 언어
- 프로그래밍 = 명령어의 모음(집합)
- 언어 = 자신의 생각을 전달하기 위해 사용하는 체계, 문법적으로 맞는 말의 집합<br>
    #### --> 프로그래밍 언어 = 컴퓨터에게 명령하기 위한 약속


# 자료형(Data Type)
## 객체와 변수
### 객체(Object)
>값을 가지고 있는 모든 것

### 변수
>객체를 담을 수 있는  빈 박스
- 객체를 참조하기 위해 사용되는 이름
- 변수는 할당 연산자(=)를 통해 값을 할당
- type
    - 변수에 할당된 값의 타입
- id
    - 변수에 할당된 값의 고유한 값

### 변수 할당
- 같은 값을 동시에 할당할 수 있음
    ```python
    x = y = 1004
    ```
- 다른 값을 동시에 할당할 수 있음
    ```python
    x, y = 1, 2
    ```

### 식별자(Identifiers)
- 파이썬 객체를 식별하는 데 사용하는 이름
- 규칙
    1. 식별자의 이름은 영문 알파벳, 언더스코어(_), 숫자로 구성
    2. 첫 글자에 숫자가 올 수 없음
    3. 길이 제한이 없고, 대소문자를 구별
    4. 예약어(True, False, and 등)는 식별자로 사용 불가능

### 자료형
- 숫자: int, float, complex, boolean
- 시퀀스: String, Tuple, List, Range
- 컬렉션: Set, Dictionary
- None

## 수치형
### 정수(Int)
- 모든 정수의 타입은 int
- 오버플로우가 발생하지 않음

### 실수(Float)
- 정수가 아닌 모든 실수
- 부동소수점
    - 실수를 컴퓨터가 표현하는 방법인 2진수(비트)로 숫자를 표현
    - 이 과정에서 floating point roudning error가 발생
        ```python
        3.14 - 3.02 == 0.12
        > false
        ```

### 불린형(BooleanType)
- True / False 값을 가진 타입
    - False는 0에, True가 아닌 수는 1에 해당
- 비교/논리 연산에서 활용

## 연산자(Operator)
### 산술 연산자
- 기본적인 사칙연산 및 수식 계산

### 복합 연산자
- 연산과 할당이 함께 이뤄짐
    ```python
    a += b #<= a = a + b
    ```

### 비교 연산자
- 값을 비교하며 True/ False 값을 반환

### 논리 연산자
- 논리식을 판단하여 True / False 값을 반환

|연산|결과|
|----|---|
|A and B|A와 B 모두 True일 때 True|
|A or B|A 와 B 모두 False일 때 False|
|Not|True를 False로, False를 True로|

## 컨테이너(Container)
- 여러 개의 값을 담을 수 있는 객체
- 시퀀스: 문자열, 리스트, 튜플, 레인지
- 컬렉션/비시퀀스: 세트, 딕셔너리

### 시퀀스형 주요 공통 연산자
|연산|결과|
|----|---|
|s[i]| s의 i번째 항목|
|s[i:j]| s의 i부터 j까지 슬라이스|
|s[i:j:k]| s의 i부터 j까지 스텝 k의 슬라이스|
|s + t| s와 t 이어 붙이기|
|s * n| s를 n번 반복|
|x in s| s의 항목 중 x와 같은 것이 있으면 True, 아니면 False|
|x not in s| s의 항목 중 x와 같은 것이 있으면 False, 아니면 True|
|len(s)| s의 길이|
|min(s)| s의 가장 작은 항목|
|max(s)| s의 가장 큰 항목|

### 문자열(String Type)
- 모든 문자는 str 타입
- 작은 따옴표(')나 큰 따옴표(")를 활용하여 표기
    - 소스코드 내에서 하나의 문장부호로 통일
- 인덱싱
    - 인덱스를 통해 특정 값에 접근할 수 있음
    - 인덱스는 0부터 시작
        ```python
        s = 'abcdefg'
        print(s[1]) # => 'b'
        ```
- 슬라이싱
    - 마지막 인덱스는 포함하지 않음
        ```python
        s = 'abcdefg
        print(s[2:5]) # => 'cde'
        ```
- 결합
    ```python
    'hello, ' + 'python'
    # 'hello, python'
    ```
- 반복
    ```python
    'hi' * 3
    # 'hihihi'
    ```
- 포함
    ```python
    'a' in 'apple'
    # True
    'b' in 'apple'
    # False
    ```
- Escape sequence
    - 문자열 내에서 특정 문자나 조작을 위해서 역슬래시를 활용
        ```python
        \n # 줄바꿈
        print('이 다음은\n엔터.')
        # 이 다음은
        # 엔터.
        ```
- 문자열은 변경 불가능, 반복 가능

### 리스트(List)
- **변경 가능**한 값들의 나열된 자료형
- 순서를 가지고 서로 다른 타입의 요소를 가질 수 있음
- 변경 가능, 반복 가능
- 대괄호([])로 생성
  ```python
  new_list = []
  ```
- 리스트 값 추가 / 삭제
    ```python
    numbers = [1, 2, 3, 4]
    numbers.append(5)
    numbers #[1, 2. 3, 4, 5]
    numbers.pop(1)
    numbers #[1, 3, 4, 5]
    ```

### None
- 값이 없음을 표현하기 위한 타입

### String Interporlation
```python
name = '은비'
age = 26
print(f'이름은 {name}이고, {age}살 입니다.')
#이름은 은비이고, 26살 입니다.
```

# 형변환
#### 암시적 형변환
- 사용자가 의도하지 않고 파이썬 내부적으로 자료형을 변환하는 경우
    ```python
    True + 3
    # 4
    3 + 5.0
    # 8.0
    ```
### 명시적 형변환
- 특정 함수를 활용하여 의도적으로 자료형을 변환하는 경우
    ```python
    '3' + 4
    # Typeerror
    int('3') + 4
    # 7
    ```