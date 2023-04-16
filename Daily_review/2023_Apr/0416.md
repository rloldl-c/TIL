# 오늘 한 일
## JavaScript - resize event
```javascript
window.addEventListener('resize', function() {
  console.log('resize')
})
```
- resize 이벤트는 resize가 일어날 때마다 코드를 실행
- 매 resize마다 코드 실행이 필요한 경우가 아니라면 비효율적
- setTimeout()메소드로 resize가 끝날 때만 코드 실행하기
```javascript
let delay = 300
let timer = null

window.addEventListener('resize', function() {
  clearTimeout(timer)
  timer = setTimeout(function() {
    console.log('resize')
  }, delay)
})
```
- 0.5초가 지나기 전에 resize가 일어나면 timer가 리셋되면서 코드가 실행되지 않음
- 0.5초동안 resize가 일어나지 않아야 코드가 실행

<br>

### `setTimeout()`
```javascript
const timeoutID = setTimeout(function[, delay]);
```
- function: 타이머가 만료된 뒤 실행할 함수
- delay: 주어진 함수를 실행하기 전에 기다릴 시간(밀리초 단위)
  - 생략하거나 0을 지정할 경우 즉시 실행
```javascript
setTimeout(function() {
  console.log('stranger!')
}, 2000)

console.log('Hello, ')
// 실행결과
// Hello,
// (2초 후)
// stranger!
```

<br>

### `clearTimeout()`
- 이전에 설정한 타이머를 취소
```javascript
const timer = setTimeout(function() {
  console.log('stranger!')
}, 2000)

clearTimeout(timer)

console.log('Hello, ')
// 실행결과
// Hello,
```