# Objects
## Function
### 1. 선언식
``` javascript
function name([param[, param[, ... param]]]) {
  statements
  return value
}
```
### 2. 표현식
``` javascript
const name = function () {
  statements
  return value
}
```
- 이름이 없는 익명 함수
- 호이스팅 되지 않으므로 함수 정의 전에 사용 불가

<br>

### 기본값 매개변수
- 값이 없거나 `undefined`가 전달될 경우 매개변수를 기본값으로 초기화
``` javascript
function multiply(a, b = 1) {
  return a*b
}

multiply(5, 2)          // 10
multiply(5)             // 5
multiply(5, undefined)  // 5
```

<br>

### 매개변수와 인자의 개수 불일치
- 매개변수 < 인자
```javascript
const noArgs = function () {
  return 0
}

console.log(noArgs(1, 2, 3)) // 0

const twoArgs = function (num1, num2) {
  return [num1, num2]
}

console.log(twoArgs(1, 2, 3)) // [1, 2]
```
- 매개변수 > 인자
```javascript
const threeArgs = function (num1, num2, num3) {
  return [num1, num2, num3]
}

console.log(threeArgs(1)) // [1, undefined, undefined]
```

<br>

### 나머지 매개변수
- 개수가 정해지지 않은 매개변수를 받을 때 사용
- 한 함수에서 하나만 사용 가능
- 마지막에 위치해야 함
``` javascript
function myFun(a, b, ...manyMoreArgs) {
  console.log("a", a);
  console.log("b", b);
  console.log("manyMoreArgs", manyMoreArgs);
}

myFun("one", "two", "three", "four", "five", "six");

// a, one
// b, two
// manyMoreArgs, [three, four, five, six]
```
<br>

### 화살표 함수 표현식
- 함수 표현식의 간결한 표현 방법
```javascript
const arrow1 = function (name) {
  return `hello, ${name}`
}

// 1. function 키워드 삭제 후 화살표로 표현 가능
const arrow2 = (name) => { return `hello, ${name}` }

// 2. 함수 바디에 return을 포함한 표현식이 1개일 경우에 중괄호와 return 삭제 가능
const arrow3 = (name) => `hello, ${name}`

// 인자가 없다면 () or _ 로 표시 가능
const noArgs1 = () => 'No args'
const noArgs2 = _ => 'No args'

// object를 return하는 경우엔 return을 작성하거나 소괄호로 대신 작성
const returnObject1 = () => { return {key: 'value'}}
const returnObject2 = () => ( {key: 'value'})
```
<br>

## Object
- 키로 구분된 데이터 집합을 저장하는 자료형
- 중괄호를 이용해 작성
- 중괄호 안에는 `key: value` 쌍으로 구성된 속성(property)를 여러 개 넣을 수 있음
- key는 문자형, value는 모든 자료형
```javascript
const user = {
  name: 'Sophia',
  age: 30,
  'key with space': true,
} // trailing comma: 속성을 추가, 삭제, 이동하기에 용이함
```
<br>

### 객체 속성
```javascript
// 조회
console.log(user.age) // 점 표기법
console.log(user['age']) // 대괄호 표기법
user['key with space'] // 공백이 포함된 key는 대괄호 표기법만 가능

user.address = 'korea' // 기존에 없는 키면 추가
user.age = 20 // 기존에 있는 키면 수정

// 삭제
delete user.address

// in
console.log('age' in user) // true
console.log('country' in user) // false
```
- 키 이름과 값으로 쓰이는 변수의 이름이 같은 경우 단축 구문 사용 가능
```javascript
const age = 30
const address = 'korea'

const newUser = {
  age,
  address,
}
```
- 고정 값이 아닌 변수 값도 사용 가능
```javascript
const product = prompt('물건 이름을 입력해주세요')
const prefix = 'my'
const suffix = 'property'
const bag = {
  [product]: 5,
  [prefix + suffix]: 'value'
}
console.log(bag) // {연필: 5, myproperty: 'value'}
```
<br>

### 메서드
- 객체의 속성 값으로 정의된 함수
```javascript
const person = {
  name: 'Sophia',
  greeting: function () {
    return 'Hello'
  },
}
// greeting 메서드 호출
console.log(person.greeting()) // Hello
```
### `this`
- 메서드 내에서 현재 객체를 참조 가능
```javascript
const person = {
  name: 'Sophia',
  greeting: function () {
    return `Hello my name is ${this.name}`
  },
}
// greeting 메서드 호출
console.log(person.greeting()) // Hello my name is Sophia
```
- 호출 방법에 따라 참조하는 값이 달라짐
``` javascript
// 단순 호출
const myFunc = function () {
  return this
}
console.log(myFunc()) // window(전역 객체)

// 메서드 호출
const myObj = {
  data: 1,
  myFunc: function () {
    return this
  }
}
console.log(myObj.myFunc()) // myObj(메서드를 호출한 객체)
```
- nested 함수에서의 문제점
``` javascript
const myObj2 = {
  numbers: [1, 2, 3],
  myFunc: function () {
    this.numbers.forEach(function (number) {
      console.log(number) //1 2 3
      console.log(this) //window
      // forEach로 들어간 함수는 일반 호출이기 때문에 this는 전역 객체를 참조
    })
  }
}

const myObj3 = {
  numbers1: [1, 2, 3],
  myFunc: function () {
    this.numbers.forEach((number) => {
      console.log(number) //1 2 3
      console.log(this) //myObj3
      // 화살표 함수는 내부 this를 가지지 않아서 외부 this 값을 그대로 사용
    })
  }
}
```
<br>

## Array
- 순서가 있는 데이터 집합을 저장하는 자료구조
- 대괄호를 이용해 작성
- 요소의 자료형엔 제약이 없음
```javascript
const fruits = ['apple', 'banana', 'coconut',]
```
### 메서드
|메서드|기능|역할|
|----|---|---|
|`push` / `pop`|배열 마지막에 요소를 추가 / 제거 |추가 / 제거|
|`unshift` / `shift`|배열 처음에 요소를 추가 / 제거|추가 / 제거|
|`forEach`|인자로 주어진 콜백 함수를 요소 각각에 대해 실행|반복|
|`map`|배열 요소 전체를 대상으로 콜백 함수를 호출하고, 결과를 배열로 반환|변형|
- 콜백 함수(Callback function): 다른 함수에 인자로 전달되는 함수
- `forEach`
```javascript
// 기본 구조
array.forEach(function (item, index, array) {
    // function body
})

const fruits = ['apple', 'banana', 'coconut',]

fruits.forEach(function (item, index, array) {
    console.log(`${item} / ${index} / ${array}`)
})
// apple / 0 / apple, banana, coconut
// banana / 1 / apple, banana, coconut
// coconut / 2 / apple, banana, coconut

fruits.forEach((item, index, array) => {
    console.log(`${item} / ${index} / ${array}`)
})
// 동일한 결과
```
- `map`
    - `forEach`와 동작 원리는 같지만 새로운 배열을 반환
``` javascript
// 기본 구조
const result = array.map(function (item, index, array) {
    // function body
})

const fruits = ['apple', 'banana', 'coconut']
const result = fruits.map((element) => {
    return element.length
})
console.log(result) // [5, 6, 7]

const numbers = [1, 2, 3]
const doubleNumber = numbers.map((number) => {
    return number * 2
})
console.log(doubleNumber) // [2, 4, 6]
```