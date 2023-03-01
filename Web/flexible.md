- flex item: flex box로 움직이는 요소들
- 가로가 메인축인 왼쪽에서 오른쪽으로 배치되는 방향이 기본 방향
- main은 가로, cross는 세로로 외우면 안됨
    - 메인축이 수직으로 바뀌면 cross가 수평이 되는 것
- flex container: flex item의 부모 요소
    - 1차 자식요소들을 컨트롤
- align-item: 행 하나를 움직이는 속성
- align-self: 개별 item을 정렬
    - 부모가 아닌 flex item에 작성

- `content` : 여러행
- `items` : 행 하나
- `self` : item 하나

- flex-grow는 비율이 아님


# Flexbox
- 요소를 행과 열 형태로 배치하는 1차원 레이아웃 방식

### 1. main axis(주축)
- flex item들이 배치되는 기본 축
- main start에서 시작하여 main end 방향으로 배치
- main axis 기본값은 row, main start는 왼쪽, main end는 오른쪽

### 2. cross axis(교차 축)
- main axis에 수직인 축
- cross start에서 시작하여 cross end 방향으로 배치
- main axis가 column이면 cross axis가 row이므로 main axis는 무조건 row, cross axis는 column 이런 식으로 이해하면 안됨

### 3. flex container
- `display: flex` 혹은 `display: inline-flex`가 설정된 부모요소
- 이 컨테이너의 1차 자식 요소들이 flex item
- flexbox 속성 값을 사용하여 자식 요소 flex item을 배치
    - flex item에 작성하는 것이 아니라 flex container에 작성된 속성 값들이 flex item에 적용되는 것

<br>

## Flexbox 속성
### 1. flex container 지정
```css
.container {
    height: 500px;
    border: 1px solid black;
    display: flex;
}
```
- flex item은 행으로 나열
- flex item은 주축의 시작선부터 나열
- flex item은 교차축의 크기를 채우기 위해 늘어남

### 2. flex-direction 지정
``` css
flex-direction: row; /* (기본값) container의 왼쪽 끝에서 오른쪽 끝 방향으로 나열*/
flex-direction: row-reverse; /* container의 오른쪽 끝에서 왼쪽 끝 방향으로 나열 */
flex-direction: column; /* container의 맨 위에서 맨 아래 방향으로 나열 */
flex-direction: column-reverse; /* container의 맨 아래에서 맨 위 방향으로 나열 */
```

### 3. flex-wrap
```css
flex-wrap: wrap;
```
- `flex-wrap: nowrap`이 기본값
- flex container에 들어가지 않는 flex item이 있는 경우 다른 행에 배치할지 여부 설정

### 4. justify-content
- 주축 방향 정렬

|값|설명|
|---|---|
|`flex-start`|기본값. container의 시작부터 정렬|
|`flex-end`|item의 마지막 항목이 container 끝에서부터 정렬|
|`center`|container의 가운데 정렬(주축 기준)|
|`space-between`|item 사이에 동일한 간격을 두고 정렬|
|`space-around`|item 주위에 동일한 간격을 두고 정렬(첫 item 이전 여백과 마지막 item 이후 여백은 각 항목간 거리의 절반)|
|`space-evenly`|item 사이와 양 끝에 동일한 간격을 두고 정렬|

### 5. align-content
- item이 두 줄 이상일 때 수직축 방향 정렬
    - `flex-wrap: wrap`인 경우 포함
- `justify-content`와 동일한 속성값

### 6. align-items
- item이 하나의 행일 때 사용하는 수직축 방향 정렬

|값|설명|
|---|---|
|`stretch`|교차축 방향을 가득 채움|
|`flex-start`|container의 시작부터 정렬|
|`flex-end`|item의 마지막 항목이 container 끝에서부터 정렬|
|`center`|container의 가운데 정렬(주축 기준)|
|`baseline`|베이스 라인을 기준으로 정렬|

### 7. align-self
- item 하나일 때 사용하는 수직축 방향 정렬 속성

<br>

## Flex item 속성
### 1. flex-basis
- flex item의 최소 크기 설정
    - item이 `flex-basis` 값보다 작을 때만 적용

### 2. flex-grow
- 행의 여백을 비율에 따라 flex item에 분배
``` css
.item1 {
    flex-grow: 1;
}

.item1 {
    flex-grow: 2;
}

.item1 {
    flex-grow: 1;
}
/*
여백이 200px인 경우
item1에 50px, item2에 100px, item3에 50px
*/
```

### 3. flex-shrink
- item이 container보다 클 때 item 크기를 축소시키는 속성
``` css
flex-shrink = 0; /* 아이템이 flex-basis 값보다 작아지지 않음 */
```

<br>

## Shorthand
### flex
``` css
flex: 1;
/* flex-grow: 1; flex-shrink: 1; flex-basis: 0%; */
flex: 1 1 auto;
/* flex-grow: 1; flex-shrink: 1; flex-basis: auto; */
flex: 1 500px;
/* flex-grow: 1; flex-shrink: 1; flex-basis: 500px; */
```

### flex-flow
``` css
/* flex-flow: <'flex-direction'>과 <'flex-wrap'> */
flex-flow: row nowrap;
flex-flow: column wrap;
flex-flow: column-reverse wrap-reverse;
```