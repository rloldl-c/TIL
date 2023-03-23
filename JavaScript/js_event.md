# Event
## event handler
- 이벤트가 발생했을 때 실행되는 함수
- 사용자의 행동에 어떻게 반응할지를 JS 코드로 표현한 것
<br>

## `.addEventListener()`
- `EventTarget.addEventListener(type, handler)`
- 특정 이벤트를 DOM 요소가 수신할 때마다 콜백 함수를 호출
- type: 이벤트 이름('click', 'input' 등)
- handler: 발생한 이벤트 객체를 수신하는 콜백 함수
    - 콜백 함수는 발생한 이벤트 객체를 유일한 매개변수로 받음
<br>

### click 이벤트
- 버튼을 클릭하면 숫자가 1씩 증가하는 이벤트
``` javascript
// 초기값 할당
let cnt = 0

// 요소 선택
const btn = document.querySelector('#btn')

// 이벤트 핸들러
btn.addEventListener('click', (event) => {
  // 버튼에 클릭 이벤트가 있을 때 실행할 코드
  cnt += 1
  const counter = document.querySelector('#counter')
  counter.textContent = cnt
})
```
<br>

### input 이벤트
- 입력하는 값 출력하기
```javascript
// 요소 선택
const inputTag = document.querySelector('#text-input')
const pTag = document.querySelector('p')

// 이벤트 핸들러
inputTag.addEventListener('input', (event) => {
    // event.target.value : input 태그에 작성되고 있는 내용
    pTag.textContent = event.target.value
})
```
<br>

### 이벤트 취소
- 텍스트 복사 방지
``` javascript
const h1Tag = document.querySelector('h1')

h1Tag.addEventListener('copy', (event) => {
  event.preventDefault()
  alter('복사할 수 없습니다.')
})
```
<br>

### lodash
- 모듈성, 성능 및 추가 기능을 제공하는 JS 유틸리티 라이브러리
- array, object 등 자료구조를 다룰 때 사용하는 유용하고 간편한 함수를 제공
#### 랜덤 번호 추첨 프로그램
``` javascript
// 아래 링크를 import 하고 사용
// <script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>

const h1Tag = document.querySelector('h1')
const btnTag = document.querySelector('#btn')
const divTag = document.querySelector('div')

btnTag.addEventListener('click', (event) => {
  const ulTag = document.createElement('ul')
  const numbers = _.range(1, 46)
  const lottoNumbers = _.sampleSize(numbers, 6)
    
  lottoNumbers.forEach((num) => {
  const liTag = document.createElement('li')
  liTag.textContent = num
  ulTag.appendChild(liTag)
  });
  divTag.appendChild(ulTag)
})
```