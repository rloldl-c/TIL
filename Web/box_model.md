# Box Model
- 모든 HTML 요소를 박스로 표현
- 박스에 대한 크기, 여백, 테두리 등의 스타일을 지정하는 디자인 개념

<br>

## Box의 구성
### 1. Content
- 콘텐츠가 표시
- `width`와 `height` 속성으로 크기 지정 가능

### 2. Padding
- content를 둘러싼 영역
- 0 이상의 값만 가능
```css
/* 네 면 모두 1em */
padding: 1em;

/* top, bottom 5% | left, right 10% */
padding: 5% 10%;

/* top 1em | left, right 2em | bottom 2em */
padding: 1em 2em 2em;

/* top 5px | right 1em | bottmo 0 | left 2em */
padding: 5px 1em 0 2em;

```

### 3. Border
- padding을 둘러싼 영역
- 스타일을 지정하지 않으면 기본값이 `none`이 적용돼 보이지 않음
- 스타일 종류

    |스타일|설명|
    |----|----|
    |`none`| 테두리 표시 X
    |`hidden`| 테두리 표시 X
    |`dotted`|둥근 점 여러개
    |`dashed`|직사각형 여러개
    |`solid`|하나의 직선
    |`double`|두 개의 평행한 직선
    |`groove`|파인 것처럼 보임
    |`ridge`|튀어나온 것처럼 보임
    |`inset`|파인 것처럼 보임
    |`outset`|튀어나온 것처럼 보임

```css
/* 스타일 */
border: solid;

/* 너비 | 스타일 */
border: 2px dotted;

/* 스타일 | 색 */
border: outset #f33;

/* 너비 | 스타일 | 색 */
border: medium dashed green;
```

### 4. Margin
- 가장 바깥쪽 레이어
- 해당 박스와 다른 요소 사이 공백 역할
- 박스로부터 다른 요소를 밀어냄
```css
/* 네 면 모두 1em */
margin: 1em;

/* top, bottom 5% | left, right center*/
margin: 5% auto;

/* top 1em | left, right center | bottom 2em*/
margin: 1em auto 2em;

/* top 2px | right 1em | bottom 0 | left auto(right alignment)*/
margin: 2px 1em 0 auto;
```
- 상쇄: top, bottom margin이 겹칠 경우 제일 큰 margin으로 결합(상쇄)

<br>

## Box Sizing
```css
.box {
  box-sizing: border-box;
  width: 350px;
  height: 150px;
  margin: 25px;
  padding: 25px;
  border: 5px solid black;
}
```
- 표준 박스 모델을 사용하면 박스가 차지하는 공간은 너비 410px(content 350 + padding 25 * 2 + border 5 * 2), 높이 210px(height 150 + padding 25 * 2+ border 5 * 2)
    - 박스 영역은 border까지 포함 ➡ margin은 박스 외부 영역에 포함
- `box-sizing: border-box;`를 설정하면 실제 content 영역만 박스에 포함

<br>

## Box type
### 1. Block
- 항상 새로운 행부터 시작
- `width`와 `height`으로 너비와 높이 지정 가능
- `width`를 지정하지 않는 경우 inline 방향으로 연장되어 사용 가능한 공간을 모두 차지(너비를 사용 가능한 공간의 100%로 채운다는 의미)
- border, padding, margin으로 다른 요소들이 밀려남
- `<h1>` ~ `<h6>`, `<p>`, `<div>` 등

### 2. Inline
- 새로운 행으로 나누어지지 않음
- `width`와 `height` 값이 적용되지 않고 콘텐츠의 너비와 높이만 차지
- border, padding, margin이 적용 되지만 다른 요소를 밀어내지 않음
    - left, right은 밀어냄
- `<a>`, `<span>`, `<img>` 등

### 3. Inline-block
- inline 요소와 block 요소 중간을 제공
- 줄바꿈 되는 것을 원하지 않으면서 너비와 높이를 적용하고 싶은 경우 사용
- border, padding, margin으로 다른 요소가 밀려남