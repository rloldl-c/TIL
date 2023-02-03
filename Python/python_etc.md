## 조건 표현식
`<true인 경우 값> if <expression> else <false인 경우 값>`
```python
num = 2
result = "홀" if num % 2 else "짝"

# if num % 2:
#     result = "홀"
# else:
#     result = "짝"

print(result)
```
## enumerate 순회
- 인덱스와 객체를 쌍으로 담은 열거형 객체 반환
```python
members = ["민수", "영희", "철수"]

for i, member in enumberate(members):
    print(i, member)

# for i in range(len(members))
#     print(f"{i} {members[i]}")

list(enumberate(members))
# [(0, "민수"), (1, "영희"), (2, "철수")]
list(enumberate(members), start=1)
# [(1, "민수"), (2, "영희"), (3, "철수")]
```

## List Comprehension
`<expression> for <변수> in <iterable>`<br>
`<expression> for <변수> in <iterable> if <조건식>`
```python
[i**3 for i in range(1, 4)]

# arr = []
# for i in range(1, 4):
#     arr.append(i**3)
# print(arr)
```
## Dictionary Comprehension
`{key: value for <변수> in <iterable}`<br>
`{key: value for <변수> in <iterable} if <조건식>`
```python
{number: number**3 for i in range(1, 4)}

# dict = {}
# for i in range(1, 4):
#     dict[i] = i**3
# print(arr)
```

## lambda
`lambda [parameter] : 표현식`<br>
- 표현식을 계산한 결과값을 반환하는 함수
- 간편 조건문 외 조건문이나 반복문을 가질 수 없음
```python
(lambda x: x + 10)(1)
# 11
```
