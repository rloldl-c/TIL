## 반복문
--------------------------------
### for문
```python
for <변수명> in <iterable>:
    # Code block
``` 
- 순회 가능한 객체(iterable) 요소를 모두 순회
  - 순회 가능한 객체: 문자열, 리스트, 레인지 등
  - 별도의 종료 조건 없이 처음부터 끝까지 모두 순회

`ex) 문자열 순회`
```python
a = 'apple'

# 각 요소만 필요할 때
for char in a:
    print(char)

# 인덱스가 필요할 때
for i in range(len(a)):
    print(a[i])
```
-------------------------------
### 반복문 제어
1. break: 반복문을 종료
    ```python
    n = 0
    while True
      if n == 3:
        break
      print(n)
      n += 1
    # 0
    # 1
    # 2
    ```
2. continue: continue 이후의 코드 블록은 실행하지 않고 다음 반복을 실행
    ```python
    for i in range(6):
        if i % 2 == 0:
            continue # 짝수인 경우 print(i)를 수행하지 않고 다음 반복으로
        print(i)
    # 1
    # 3
    # 5
    ```
3. for-else
  - 반복문을 끝까지 실행한 후 else문 실행
    ```python
    for char in 'apple':
      if char == 'b':
        print('b!')
        break
    else:
      print('b가 없습니다.')
    # b가 없습니다.
    ```
  - break로 중간에 종료되면 else문은 실행되지 않음
    ```python
    for char in 'banana':
      if char == 'b':
        print('b!')
        break
    else:
      print('b가 없습니다.')
    # b!
    ```
---------------------------

### while문
```python
while < expression >:
  # Code block
```
- 조건식이 참인 경우 반복적으로 코드를 실행
- 코드 블록이 실행되고, 다시 조건식을 검사하여 반복적으로 실행
- 무한 루프를 하지 않도록 종료 조건이 반드시 필요
  ```python
  a = 0
  while a < 5:
    print(a)
    a += 1 # 종료조건
  ```
`ex) 1부터 사용자가 입력한 양의 정수까지 총합을 구하는 코드`
```python
n = int(input())
total = 0
cnt = 0

while cnt <= n:
  total += cnt
  cnt += 1
print(total)

# for문 코드
# for cnt in range(n + 1):
#   total += cnt
# print(total)
```

