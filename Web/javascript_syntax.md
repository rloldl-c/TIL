# JavaScript Syntax
## 변수 선언
### 1. `let`
- 블록 스코프를 갖는 지역 변수를 선언
- 초기화를 하지 않으면 `undefined`로 초기화
- 재할당 가능, 재선언 불가능
``` javascript
let number = 10 // 선언 및 초기화
number = 20 // 재할당 가능
let number = 5 // 재선언 불가능
```

### 2. `const`
- 블록 스코프를 갖는 지역 변수를 선언
- 초기화를 하지 않으면 선언 자체가 불가능
- 재할당 불가능, 재선언 불가능
``` javascript
const number = 10 // 선언 및 초기화
number = 20 // 재할당 불가능
const number = 5 // 재선언 불가능
```

#### * 블록 스코프(block scope)
- 중괄호({})로 묶인 내부
- `let`과 `const`로 선언한 요소는 블록 바깥에서 접근 불가능
``` javascript
let x = 1
{
  let x = 2
}
console.log(x) // 1이 콘솔에 출력

const c = 1
{
  const c = 2
}
console.log(c) // 1이 콘솔에 출력
```

<br>

## 데이터 타입
### 원시 자료형(Primitive type)
- 변수에 값이 직접 저장되는 자료형(불변, 값이 복사)
- Number, String, Boolean, undefined, null
``` javascript
let a = 10
let b = a
b = 20

console.log(a) // 10
console.log(b) // 20
```
<br>

#### 1. Number
- 정수 또는 실수형 숫자를 표현하는 자료형
``` javascript
const a = 3
const b = -5
const c = 3.14
const d = Infinity
const e = -Infinity
const f = NaN // Not a Number
```
- `NaN`을 반환하는 연산
    - 숫자로 나타낼 수 없는 것
    - 결과가 허수인 계산식
    - 정의할 수 없는 계산식
    - 피연산자가 `NaN`
    - 유효하지 않은 값이 숫자로 표시되는 경우(잘못된 날짜 등)

#### 2. String
``` javascript
const firstName = 'Tony'
const secondName = 'Stark'
const fullName = firstName + secondName // 문자열끼리 덧셈 가능
```
- Template Literal: 문자열 사이에 변수 삽입하기
    - 따옴표(')가 아닌 백틱(`) 사용
``` javascript
const age = 10
const message = `홍길동은 ${age}세입니다.`
```

#### 3. null
- 변수의 값이 없음을 의도적으로 표현할 때 사용
``` javascript
const lastName = null
```

#### 4. undefined
- 변수 선언 이후 값을 할당하지 않으면 자동으로 할당되는 값
``` javascript
let lastName
console.log(lastName) // undefined 출력
```

#### 5. Boolean
- 조건문 또는 반복문에서 boolean이 아닌 데이터 타입은 자동으로 `true` 또는 `false`로 변환

|데이터 타입|true|false|
|---|:----:|----|
|undefined|X|항상 false|
|null|X|항상 false|
|Number|false를 제외한 모든 경우|0, -0, NaN|
|String|false를 제외한 모든 경우|빈 문자열|

<br>

### 참조 자료형(Reference type)
- 객체의 주소가 저장되는 자료형(가변, 주소가 복사)
- Objects, Array, Function
``` javascript
const obj1 = { name: 'Alice', age: 30}
const obj2 = obj1
obj2.age = 40

console.log(obj1.age) // 40
console.log(obj2.age) // 40
```

<br>

## 연산자
### 비교 연산자
- 피연산자들을 비교하고 결과값을 boolean으로 반환
``` javascript
3 < 2 // false
'A' < 'B' // true
```

### 동등 연산자(==)
- 두 피연산자가 같은 값인지 비교 후 boolean 값을 반환
- 비교할 때 암묵적 타입 변환으로 타입을 일치시킨 후 비교
- 두 피연산자가 모두 객체일 경우 메모리의 같은 객체를 바라보는지 판별

### 일치 연산자(===)
- 두 피연산자의 값과 타입이 모두 같은 경우 true를 반환
- 같은 객체를 가르키거나, 같은 타입이면서 같은 값인지를 비교
- 암묵적 타입 변환이 발생하지 않음
``` javascript
const a = 1
const b = '1'

console.log(a === b) // false
console.log(a === Number(b)) // true
```

### 논리 연산자

|논리값|연산자|
|---|---|
|and|`&&`|
|or|`\|\|`|
|not|`!`|
```javascript
false && true // false
false || true // true
!false // true
```
<br>

## 조건문
```javascript
if (조건1) {
  명령문1
}
else if (조건2) {
  명령문2
}
else {
  명령문N
}
```
<br>

## 반복문
### `while`
- 조건문이 참이기만 하면 문장을 계속해서 수행
```javascript
let n = 0;
let x = 0;

while (n < 3) {
  n++;
  x += n;
}
// 첫 번째 반복: n = 1, x = 1
// 두 번째 반복: n = 2, x = 3
// 세 번째 반복: n = 3, x = 6
// 이후로는 n이 3보다 커져 조건을 만족하지 못하므로 반복문 종료
```

### `for`
- 특정한 조건이 거짓으로 판별될 때까지 반복
``` javascript
for ([initialization]; [condition]; [final-expression]) {
  statement
}
```
- initialization
    - 주로 카운터 변수를 초기화하거나 `let` 키워드로 새로운 카운터 변수를 선언
- condition
    - 매 반복마다 평가할 식
    - 평과 결과가 참이라면 statement를 실행하고, 거짓이라면 for문의 다음 식으로 건너 뜀
- final-expression
    - 조건의 평과 결과가 참일 때 실행하는 구문
    - 아무것도 실행하지 않을 수 있음(공백문(`;`))
``` javascript
for (let i = 0; i < 6; i++) {
  console.log(i);
}
// 1. 반복문 진입 및 변수 i 선언
// let i = 0
// 2. 조건문 평가 후 코드 블럭 실행
// i < 6이 참이면 console.log(i) 실행
// 3. 코드 블럭 실행 후 i값 증가
// i ++
// 4. 조건문을 만족하지 못할 때까지 2-3 반복
```

### `for...in`
- 객체(object)의 속성을 순회할 때 사용
``` javascript
const fruits = { a: 'apple', b: 'banana'}

for (const key in fruits) {
  console.log(key) // a b
  console.log(fruits[key]) // apple banana
}
```

### `for...of`
- 반복 가능한 객체(배열, 문자열 등)를 순회할 때 사용
```javascript
const numbers = [0, 1, 2, 3]

for (const num of numbers) {
  console.log(num) // 0 1 2 3
}
```

### `for...in`과 `for...of`
``` javascript
const numbers = [10, 20, 30] // Array
const capitals = {
  korea: '서울',
  france: '파리',
  japan: '도쿄'
} // Object

for (const num in numbers) {
  console.log(num) // 0 1 2
} // for...in은 순서에 따른 인덱스를 보장할 수 없음 > 인덱스의 순서가 중요한 배열에서 사용 X

for (const num of numbers) {
  console.log(num) // 10 20 30
}

for (const capital in capitals) {
    console.log(capital) // korea france japan
}

for (const capital of capitals) {
    console.log(capital) // TypeError: capitals is not iterable
}
```