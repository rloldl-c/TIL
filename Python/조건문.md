# 제어문
- 특정 상황에 따라 코드를 선택적으로 실행(분기/조건)하거나 계속하여 실행(반복)하는 제어가 필요

## 조건문
- 조건문은 참/거짓을 판단할 수 있는 조건식과 함께 사용
### 기본 형식
```python
if < expression >:
    # Run this Code block
else:
    # Run this Code block
```
- expression에는 참/거짓에 대한 조건식
- else는 선택적으로 활용 가능
  - else에는 조건식 XX

`ex) 홀수/짝수 판단하는 조건문`
```python
num = int(input())
if num % 2 == 0:
    print('짝수')
else:
    print('홀수')
print(num)
```

### 복수 조건문
```python
if < expression >:
    # Run this Code block
elif < expression >:
    # Run this Code block
else:
    # Run this Code block
```
- 여러 조건식 중 true인 조건식을 찾는 것이 아니라 위에서부터 순차적으로 내려오면서 true인 조건식을 찾는 것
```python
dust = 80
if dust > 150:  # 80 > 150은 false니까 다음 조건식으로
    print('매우나쁨') 
elif dust > 80: # 80 > 80은 false니까 다음 조건식으로
    print('나쁨')
elif dust > 30: # 80 > 30은 true니까 '보통' 출력 
    print('보통')
else:
    print('좋음')
print(dust)
```

### 중첩 조건문
```python
if < expression >:
    # Code block
    if < expression >:
        # Code block
else:
    # Code block
```

## 레인지(Range)
- 숫자의 범위를 나타내기 위해 사용
1. 기본형: range(n)
  - 0부터 n-1까지의 숫자
    ```python
    list(range(4))
    # [0, 1, 2, 3]
    ```
2. 범위 지정: range(n, m)
  - n부터 m-1까지의 숫자
    ```python
    list(range(1, 5))
    # [1, 2, 3, 4]
    ```
3. 범위 및 스텝 지정: range(n, m, s)
  - n부터 m-1까지 s씩 증가시킨 숫자
    ```python
    list(range(1, 5, 2))
    # [1, 3]
    ```


