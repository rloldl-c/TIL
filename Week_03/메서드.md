# 메서드(Methods)
- 객체.메서드()
- 객체에서 실행되는 함수
- 객체를 조작할 수 있는 방법

## 문자열
### 문자열 탐색/검증
`s.find(x)`: x의 첫 번째 위치를 반환, 없으면 -1을 반환<br>
`s.index(x)`: x의 첫 번째 위치를 반환, 없으면 오류 반환<br>
`s.isalpha()`: 알파벳 문자 여부<br>
`s.isupper()`: 대문자 여부<br>
`s.islower()`: 소문자 여부<br>
`s.istitle()`: 타이틀 형식 여부<br>

### 문자열 변경
`s.replace(old, new[,count])`: 바꿀 대상 글자를 새로운 글자로 바꿔서 반환, 카운트를 지정할 경우 해당 개수만큼만 바꿔줌
```python
print('coone'.replace('o', 'a'))
# caane
print('wooooowoo'.replace('o', '!', 2))
# w!!ooowoo
```
`s.strip([chars])`: 특정 문자를 제거, 문자를 지정하지 않으면 공백만 제거
```python
print('  우와\n'.stirp())
# '우와'
print('!banana!'.lstrip('!'))
# banana!
print('!banana!'.rstrip('!'))
# !banana
```
`s.split(sep=None, maxsplit=1)`: 문자열을 특정한 단위로 나눠 리스트로 반환
```python
print('a b c'.split())
# ['a', 'b', 'c']
```
`'separator'.join([iterable])`: 구분자로 iterable을 합침
```python
print(''.join(['3', '5']))
# 35
```
`s.capitalize()`: 가장 첫 번째 글자를 대문자로 변경<br>
`s.title()`: '나 공백 이후를 대문자로 변경<br>
`s.upper()`: 모두 대문자로 변경<br>
`s.lower()`: 모두 소문자로 변경<br>
`s.swapcase()`: 대소문자를 서로 변경<br>

## 리스트
`l.append(x)`: 리스트 마지막에 항목 x를 추가<br>
`l.inser(i, x)`: 리스트 인덱스 i에 항목 x를 삽입
```python
fruits = ['apple', 'banana', 'kiwi']
fruits.insert(0, 'start')
print(fruits)
# ['start', 'apple', 'banana', 'kiwi']
fruits.insert(5, 'end')
print(frutis)
# ['start', 'apple', 'banana', 'kiwi', 'end']
```
`l.remove(x)`: 리스트 가장 왼쪽에 있는 항목 x를 제거, 항목이 존재하지 않는 경우 ValueError 발생
```python
numbers = [1, 2, 3, 'hi']
numbers.remove('hi')
print(numbers)
# [1, 2, 3]
```
`l.pop(i)`: 리스트의 인덱스 i(지정하지 않을 경우 가장 오른쪽)에 있는 항목을 반환 후 제거<br>
`l.extend(m)`: 순회형 m의 모든 항목들을 리스트 끝에 추가
```python
fruits = ['apple', 'banana', 'kiwi']
fruits.extend(['orange', 'mango'])
print(fruits)
# ['apple', 'banana', 'kiwi', 'orange', 'mango']
```
`l.index(x, start, end)`: 리스트에 있는 항목 중 가장 왼쪽에 있는 항목 x의 인덱스를 반환
  - x가 여러개여도 가장 왼쪽에 있는 인덱스 하나만 반환

`l.reverse()`: 리스트를 거꾸로 정렬
`l.sort()`: 원본 리스트를 정렬, 반환값은 None
  - sorted 함수랑 비교해본다면?
```python
numbers = [3, 2, 5, 1]
result = numbers.sort()
print(numbers, result)
# [1, 2, 3, 5] None
result = sorted(numbers)
print(numbers, result)
# [3, 2, 5, 1] [1, 2, 3, 5]
```
`l.count(x)`: 리스트에서 항목 x가 몇 개 존재하는지 갯수를 반환

## 세트
`s.copy()`: 세트의 얕은 복사본을 반환<br>
`s.add(x)`: 항목 x가 세트 s에 없다면 추가<br>
`s.pop()`: 세트 s에서 랜덤하게 항목을 반환하고 제거, 세트가 비어 있을 경우 KeyError
  - 인덱스가 없으니 랜덤으로 제거<br>

`s.remove(x)`: 항목 x를 세트 s에서 삭제, 항목이 존재하지 않는 경우 KeyError

### 세트 연산자

## 딕셔너리
`d.clear()`: 모든 항목을 제거<br>
`d.keys()`: 딕셔너리 d의 모든 키를 담은 뷰를 반환<br>
`d.values()`: 딕셔너리 d의 모든 값을 담은 뷰를 반환<br>
`d.items()`: 딕셔너리 d의 모든 키-값의 쌍을 담은 뷰를 반환<br>
`d.get(k, v)`: 키 k의 값을 반환하는데, k가 딕셔너리에 없을 경우 v(지정하지 않을 경우 None)을 반환
  - key에 직접 접근하면 KeyError가 발생하지만 get 메서드는 v을 반환
```python
my_dict = {'apple': '사과', 'banana': '바나나'}
print(my_dict.get('kiwi'))
# None
print(my_dict.get('apple'))
# '사과'
print(my_dict.get('kiwi', 0))
# 0
```
`d.pop(k, v)`: 키 k의 값을 반환하고 키 k인 항목을 딕셔너리 d에서 삭제하는데, k가 딕셔너리에 없을 경우 v(지정하지 않을 경우 None)을 반환
```python
my_dict = {'apple': '사과', 'banana': '바나나'}
data = my_dict.pop('banana')
print(data)
# {'apple': '사과'}
```
`d.update([other])`: 딕셔너리에 d의 값을 매핑하여 업데이트