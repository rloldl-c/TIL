# 함수
- 복잡한 내용을 숨기고 기능에 집중하여 사용할 수 있음
- 재사용성, 가독성, 생산성

## 함수 기초
### 함수?
- 특정한 기능을 하는 코드의 묶음
- 코드를 매번 다시 작성하지 않고, 필요시에만 호출하여 사용 가능
- 구현된 함수가 없는 경우, 사용자가 직접 작성 가능
```python
def function_name
  # code block
  return returning_value
```
--------------------------------
## 내장 함수
`len(s)`
- 객체 길이를 반환
- input은 보통 시퀀스 또는 컬렉션<br>

`sum(iterable, start=0)`
- iterable 항목들을 왼쪽에서 오른쪽으로 합하고 합계를 반환
- iterable 항목은 일반적으로 숫자이며 시작 값은 문자열이 될 수 없음<br>

`max(iterable)`
- iterable이나 두 개 이상의 input 중 가장 큰 값을 반환
- 최대값이 중복이라면 처음 만난 항목을 반환<br>

`min(iterable)`
- iterable이나 두 개 이상의 input 중 가장 작은 값을 반환
- 최소값이 중복이라면 처음 만난 항목을 반환<br>

`abs(x)`
- 절대값을 반환
- input으로는 정수, 실수 또는 __abs__()를 구현하는 객체<br>

`divmod(a, b)`
- 두 수를 받아 몫과 나머지를 반환<br>

`pow(base, exp, mod=None)`
- base의 exp 거듭제곱을 반환<br>

`round(number, ndigit=None)`
- number를 소수점 다음에 ndigit 정밀도로 반올림한 값을 반환