# 사용자 정의 함수
## 선언과 호출
- 선언은 def 키워드를 활용
- 들여쓰기를 통해 function body(실행될 코드 블럭)를 작성
- 함수는 parameter를 넘겨줄 수 있음
- 함수는 동작 후에 return을 통해 결과값을 전달
- 함수는 함수명()으로 호출
  - prarameter가 있는 경우 함수명(parameter1, parameter2, ...)로 호출

## 결과값
- 함수는 반드시 하나의 값만을 return
  - 명시적이 return이 없는 경우엔 None을 반환
```python
def minus_and_product(x, y):
    return x - y
    return x * y

minus_and_product(1, 2) # -1
```
  - return으로 두 개 이상의 값을 반환하게 작성하면 튜플로 반환
```python
def minus_and_product(x, y):
    return x - y, x * y

minus_and_product(4, 5) # (-1, 20)
```
- 함수는 return과 동시에 실행 종료

## 함수의 입력
```python
def function(ham): # parameter: ham
    return ham

function('spam') # argument: spam
```
### argument
- 함수 호출 시 함수의 parameter를 통해 전달되는 값
- argument는 소괄호 안에 할당<br>
`func_name(arguement)`
  - 필수 argument: 반드시 전달되어야 하는 argument
  - 선택 argument: 기본값이 설정되어 있어 값을 전달하지 않아도 되는 argument
- positional argument: 기본적으로 argument는 위치에 따라 함수 내에 전달
```python
def add(x, y):
    return x + y

add(2, 3) # x == 2, y == 3
```
- keyword argument: 직접 변수의 이름으로 특정 argument를 전달할 수 있음
  - keyword argument 다음에 positional argument를 활용할 수 없음
```python
def add(x, y):
    return x + y

add(x=2, y=3)
```
- default argument: 기본값을 지정하여 함수 호출시 argument 값을 설정하지 않도록 함
  - 정의된 것보다 적은 개수의 argument로도 호출될 수 있음
```python
def add(x, y=0):
    return x + y

add(2) # y=0이라는 기본값이 있어서 x만 전달되어도 함수 호출 가능
```
- 정해지지 않은 개수의 argument
  - 여러 개의 positional argument를 하나의 필수 parameter로 받아서 사용
  - argument들은 튜플로 묶여서 처리
```python
def add(*args):
    res = 0
    for arg in args:
        res += 0
    return res

add(2)
add(1, 2, 3, 4)
```
- 정해지지 않은 개수의 keyward argument
  - 함수가 임의의 개수 argument를 keyword argument로 호출될 수 있도록 지정
  - argument들은 딕셔너리로 묶여서 처리
```python
def family(**kwargs):
    for key, value in kwargs:
        print(key, ":", value)
  
famliy(father="John", mother="Jane")
```

## 함수의 범위(Scope)
- local scope: 함수가 만든 scope, 함수 내부에서만 참조 가능
  - 함수가 호출될 때 생성되고 함수가 종료될 때까지 유지
- global scope: 코드 어디에서든 참조할 수 있는 공간
  - 모듈이 호출된 시점 이후 혹은 인터프리터가 끝날 때까지 유지
- built-in scope: 파이썬이 실행된 이후부터 영원히 유지

### 이름 검색 규칙(LEGB Rule)
1. Local scope: 함수
2. Enclosed scope: 특정 함수의 상위 함수
3. Global scope: 함수 밖의 변수, import 모듈
4. Built-in scope: 파이썬 안에 내장되어 있는 함수 또는 속성
- 함수 내에서는 바깥 scope의 변수에 접근만 가능, 수정 불가능