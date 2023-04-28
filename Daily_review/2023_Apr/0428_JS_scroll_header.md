# 오늘 한 일
## JavaScript
### 스크롤을 올리면 헤더가 안 보이고 스크롤을 내리면 헤더가 내려오는 효과
``` css
/* css */
.header {
  position: absolute;
  top: 0;
  width: 100%;
  height: 4rem;
  /* 헤더가 움직이는 효과를 자연스럽게 하기 위한 transition */
  transition: top 0.3s ease-in-out;
}

.nav-up {
  /* 헤더 높이와 같은 값 */
  top: -4rem;
}
```

### 1. 스크롤 이벤트 감지
```javascript
document.addEventListener("scroll", function() {
  // body
})
```

### 2. 스크롤 방향 판단
```javascript
let prevScrollTop = 0 // 최상단 위치

document.addEventListener("scroll", function() {
  let nextScrollTop = window.pageYOffset // 현재 스크롤 위치
  if (nextScrollTop > prevScrollTop) {
    // 스크롤이 내려갈 때 실행할 코드
  } else if (nextScrollTop < prevScrollTop) {
    // 스크롤이 올라갈 때 실행할 코드
  }

  prevScrollTop = nextScrollTop
})
```
- 현재 스크롤 위치가 이전 스크롤 위치보다 크다면 스크롤이 내려가는 중 == 헤더를 숨기는 코드 작성
- 현재 스크롤 위치가 이전 스크롤 위치보다 작다면 스크롤이 올라가는 중 == 헤더가 보이게 하는 코드 작성
- 스크롤 이벤트가 발생할 때마다 이전 위치를 현재 위치로 갱신해주면서 스크롤 방향을 판단

### 3. 헤더 보이거나 숨기기
```javascript
const header = document.querySelector(".header")

// 방향에 따라 헤더를 보이거나 숨기는 함수 작성
const moving = function(direction) {
  if (direction === 'up') {
    header.classList.remove('nav-up')
  } else {
    header.classList.add('nav-up')
  }
}
```
- 스크롤이 올라가면 nav-up 클래스를 없애서 헤더가 내려오는 효과처럼 보이도록 작성
- 반대로 스크롤이 내려가면 nav-up 클래스를 추가해서 헤더가 안 보이도록 작성

### 최종 코드
```javascript
// JavaScript
const header = document.querySelector('.header')
let prevScrollTop = 0

let headerMoving = function(direction) {
  if (direction == 'up') {
    header.classList.remove('nav-up')
  } else {
    header.classList.add('nav-up')
  }
}

document.addEventListener('scroll', function() {
  let nextScrollTop = window.pageYOffset
  if (nextScrollTop > prevScrollTop) {
    headerMoving('down')
  } else if (nextScrollTop < prevScrollTop) {
    headerMoving('up')
  }

  prevScrollTop = nextScrollTop
})
```