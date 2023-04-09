# 오늘 한 일
## CSS - transform
### `translate()`
- 현재 위치에서 주어진 x축과 y축의 거리만큼 이동시킴
- 주어진 값이 양수면 해당 축의 양의 방향으로, 음수면 해당 축의 음의 방향으로 이동
```css
transform: translate(12px, 50%);
transform: translate3d(12px, 50%, 3em);
transform: translateX(2em);
transform: translateY(3in);
transform: translateZ(2px);
```

### `rotate()`
- 주어진 각도만큼 시계 방향이나 반시계 방향으로 회전
- 주어진 값이 양수면 시계 방향, 음수면 반시계 방향으로 회전
```css
transform: rotate(0.5turn);
transform: rotate3d(1, 2.0, 3.0, 10deg);
transform: rotateX(10deg);
transform: rotateY(10deg);
transform: rotateZ(10deg);
```

### `scale()`
- 요소의 크기를 주어진 배율만큼 늘리거나 줄임
- 주어진 배율이 1보다 크면 커지고, 1보다 작으면 줄어듦
```css
transform: scale(2, 0.5);
transform: scale3d(2.5, 1.2, 0.3);
transform: scaleX(2);
transform: scaleY(0.5);
transform: scaleZ(0.3);
```

### `skew()`
- 요소를 주어진 각도만큼 x축과 y축으로 기울임
- `skewX()`는 x축으로, `skewY()`는 y축으로만 기울임
- 주어진 각도가 양수면 양의 방향으로, 음수면 음의 방향으로 기울임
```css
transform: skew(30deg, 20deg);
transform: skewX(30deg);
transform: skewY(1.07rad);
```

### `matrix()`
- transform 메소드를 한 줄에 설정
```css
matrix(scaleX(), skewY(), skewX(), scaleY(), translateX(), translateY())
```
<br>

## CSS - transition
- 정해진 시간 동안 요소의 속성값을 부드럽게 변화시킴
```css
/* 마우스를 올려놓으면 div의 너비가 1초동안 3배로 늘어남 */
div {
  width: 100px;
  transition: width 1s;
}
div:hover {
  width: 300px;
}

/* 마우스를 올려놓으면 div의 너비는 1초동안, 높이는 3초동안 3배로 늘어남 */
div {
  width: 100px;
  height: 100px;
  transition: width 1s, height 3s;
}
div:hover {
  width: 300px;
  height: 300px;
}
```
### transition-timing-function
- linear: transition 효과가 처음부터 끝까지 일정한 속도로 진행
- ease: 기본값, 효과가 천천히 시작되어 빨라지다가 마지막에는 다시 느려짐
- ease-in: 효과가 천천히 시작
- ease-out: 효과가 천천히 끝남
- ease-in-out: 효과가 천천히 시작되어 천천히 끝남
- cubic-bezier(n, n, n, n): 효과가 사용자가 정의한 cubic-bezier 함수에 따라 진행

### transition-delay
- transition 효과가 나타나기 전까지 지연 시간을 설정
```css
/* 1초가 지난 뒤에야 div의 크기가 바뀌기 시작 */
div {
  height: 100px;
  width: 150px;
  transition: width 1s, height 2s;
  transition-delay: 1s;
}

div:hover { width: 300px; height: 300px; }
```

### transition-duration
- transition 효과가 지속될 시간을 설정
- 기본값이 0s라 어느 값도 지정하지 않으면 효과가 나타나지 않음
- `transition`으로 한줄에 작성 가능
```css
/* 2초동안 너비가 변함 */
transform: width 2s;
```
- `transition-property` 값이 더 많으면 `transition-duration` 값이 부족한 만큼 반복
```css
/* width 2s, opacity 1s, left 2s, top 1s */
div {
  transition-property: width, opacity, left, top;
  transition-duration: 2s, 1s;
}
```

### transition-property
- 요소에 추가할 transition 효과를 설정
- 아무것도 설정하지 않으면 모든 요소가 설정됨
```css
/* 마우스를 올려놓으면 너비는 2초동안 3배가 늘어나고, 배경색은 2초동안 파란색으로 변함 */
div {
  width: 100px;
  height: 50px;
  background-color: red;
  transition-property: width, background-color;
  transition-duration: 2s, 2s;
}
div:hover {
  width: 300px;
  background-color: blue;
}
```