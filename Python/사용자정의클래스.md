# 사용자 정의 클래스

## 객체 지향 프로그래밍
- 객체 지향 프로그래밍: 
### 객체
- 객체의 특징
  - 타입(type): 어떤 연산자(operator)와 조작(method)이 가능한가?
  - 속성(attribute): 어떤 상태(data)를 가지는가?
  - 조작법(method): 어떤 행위(function)를 할 수 있는가?

### 절차 지향 vs 객체 지향
- 절차 지향
  ```python
  def area(x, y):
    return x * y

  def circumference(x, y):
    return 2 * (x + y)

  a = 10
  b = 30
  c = 300
  d = 20
  square1_area = area(a, b)
  square1_circumference = circumference(a, b)
  square2_area = area(c, d)
  square2_circumference = circumference(c, d)
  ```
- 객체 지향
  ```python
  class Rectangle:
    def __init___(self, x, y):
      self.x = x
      self.y = y

    def area(x, y):
      return self.x * self.y

    def circumference(x, y):
      return 2 * (self.x + self.y)

    r1 = Rectangle(10, 30)
    r1.area()
    r1.circumference()
    r2 = Rectangle(300, 20)
    r2.area()
    r2.circumference()
  ```
    - Rectangle(사각형) = 클래스(class)
    - r1, r2(각 사각형) = 인스턴스(instance)
    - 10, 30,(가로 세로 길이) = 속성(attribute)
    - area, circumference =  메소드(method)

## 클래스와 인스턴스
```python
# 클래스 정의
class MyClass:
  pass

# 인스턴스 생성
my_instance = MyClass()
# 메소드 호출
my_instance.my_method()
# 속성
my_instance.my_attribute
```
- 객체의 틀(클래스)을 가지고 객체(인스턴스)를 생성한다
  - 클래스: 객체들의 분류
  - 인스턴스: 하나하나의 실체, 예
- 속성: 특정 데이터 타입/클래스들의 객체들이 가지는 실제 값/상태
- 메소드: 특정 데이터 타입/클래스들의 객체들이 공통적으로 실행할 수 있는 함수
### 객체 비교하기
1. `==`
  - 변수가 참조하는 객체의 내용이 같은 경우 True
  - 두 객체가 가진 값은 같더라도 같은 대상을 가리키는 것은 아님

2. `is`
  - 두 변수가 동일한 객체를 가리키는 경우 True

```python
a = [1, 2, 3]
b = [1, 2, 3]

print(a == b, a is b)
# True Flase

a = [1, 2, 3]
b = a

print(a == b, a is b)
# True True
```

## 인스턴스
- 인스턴스 변수
  - 인스턴스가 개인적으로 가지는 속성(attribute)
  - 각 인스턴스들의 고유한 변수
- 생성자 메소드의 `self.<name>`으로 정의
  - self: 인스턴스 자기 자신
- 인스턴스가 생성된 후 `<instance>.<name>`으로 접근 및 할당
```python
class Person:
  def __init__(self, name):
    self.name = name # 인스턴스 변수 정의

john = Person("john") # 인스턴스 변수 접근 및 할당 방법 1
print(john.name)
# john

john.name = "John Kim" # 인스턴스 변수 접근 및 할당 방법 2
print(john.name)
# John Kim
```
### 생성자 메소드
- 인스턴스 객체가 생성될 때 자동으로 호출되는 메소드
- 인스턴스 변수들의 초기값을 설정
```python
class Person:
  def __init__(self):
    print("인스턴스가 생성되었습니다.")

person1 = Person()
# 인스턴스가 생성되었습니다.
```

### 매직 메소드
- __가 있는 특수한 동작을 위해 설계된 메소드
- 특정 상황에서 자동으로 호출
```python
class Circle:
  def __init__(self, r):
    self.r = r
  
  def area(self):
    return 3.14 * self.r * self.r
  
  def __str__(self):
    return f'[원] radius: {self.r}'

  def __gt__(self, other):
    return self.r > other.r

c1 = Circle(10)
c2 = Circle(2)

print(c1) # [원] radius: 10
print(c2) # [원] radius: 1

c1 > c2 # True
c1 < c2 # False
```

## 클래스
### 클래스 변수
- 한 클래스에서 모든 인스턴스가 공통으로 가지고 있는 속성
- 클래스 선언 내부에서 정의
- `<classname>.<name>`으로 접근 및 할당
```python
class Circle
    pi = 3.14

c1 = Circle()
c2 = Circle()
print(Circle.pi)
print(c1.pi)
print(c2.pi)
# 3.14
# 3.14
# 3.14
```
### 클래스 메서드
- 클래스가 사용할 메서드
- `@classmethod` 를 사용하여 정의
- 호출시 첫번째 인자로 클래스가 전달

### 스태틱 메서드
- 인스턴스나 클래스를 사용하지 않는 메서드
- `@staticmethod` 를 사용하여 정의
- 호출시 어떠한 인자도 전달되지 않음
  - 클래스 및 인스턴스 정보에 접근/수정 불가

### 메서드 정리
- 스태틱 메서드: 인스턴스나 클래스를 조작하지 않는 경우
- 인스턴스 메서드: 인스턴스를 조작하는 경우(첫번째 인자로 전달된 인스턴스 조작)
- 클래스 메서드: 클래스를 조작하는 경우(첫번째 인자로 전달된 클래스 조작)

## 상속
- 두 클래스 사이 부모-자식 관계를 성립하는 것
- 부모에 정의된 속성이나 메서드를 활용하거나 오버라이딩(재정의)하여 활용
```python
class Person:
    def __init__(self, name):
        self.name = name
    
    def greeting(self):
        return f"안녕, {self.name}"

class Mom(Person):
    gene = "XX"

    def swim(self):
        return "엄마가 수영"

class Dad(Person):
    gene = "XY"

    def walk(self):
        return "아빠가 걷기"

class FirstChild(Dad, Mom):
    def swim(self):
        return "첫째가 수영"

    def cry(self):
        return "첫째가 응애"

class SecondChild(Mom, Dad):
    def swim(self):
        return "둘째가 수영"

    def cry(self):
        return "둘째가 응애"

baby1 = FirstChild("아가")
baby1.cry() # 첫째가 응애
baby1.swim() # 첫째가 수영
baby1.walk() # 아빠가 걷기
baby1.gene() # XY

baby2 = SecondChild("애기")
baby2.cry() #둘째가 응애
baby2.swim() #둘째가 수영
baby2.walk() # 엄마가 걷기
baby2.gene() # XX
```
