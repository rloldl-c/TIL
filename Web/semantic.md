# Semantic
## HTML
- 기본적인 모양과 기능 이외에 의미를 가지는 HTML 요소
- 검색엔진 및 개발자가 웹 페이지의 콘텐츠를 이해하기 쉽게 만들어줌
``` css
<h1>Heading</h1>
<span style="font-size: 32px;">Heading</span>
```
- 모든 요소를 `h1` 태그처럼 보이게 할 수는 있으나 의미론적 가치는 없음

### 의미론적 마크업의 이점
- 검색 엔진이 의미론적 마크엄을 통해 중요한 키워드를 판단
- 화면 리더기로 페이지를 탐색할 때 의미론적 마크업을 푯말로 사용

### 대표적인 sematic element
- `header`
- `nav`
- `main`
- `article`
- `section`
- `aside`
- `footer`

<br>

## CSS
### OOCSS
- 객체 지향적 접근법을 적용하여 CSS를 구성하는 방법론
```css
<head>
...
    <style>
    /* 기본 카드 구조 */
    .card {
      border: 1px solid black;
      border-radius: 5px;
      padding: 1rem;
    }

    /* 카드 제목 */
    .card-title {
      font-size: 1rem;
      font-weight: bold;
    }

    /* 카드 내용 */
    .card-description {
      font-size: 0.7rem;
    }

    /* 기본 버튼 구조 */
    .btn {
      padding: 1rem;
      cursor: pointer;
    }

    .bg-red {
      background-color: crimson;
    }

    .bg-blue {
      background-color: lightblue;
    }
  </style>
</head>
<body>
  <div class="card">
    <p class="card-title">Card Title</p>
    <p class="card-description">This is a card description.</p>
    <button class="btn bg-red">Learn More</button>
    <button class="btn bg-blue">Learn More</button>
  </div>
</body>
...
```

### BEM
- Block, Element, Modifier를 사용해 클래스 이름을 구조화하는 방법론
1. Block
    - `.block`
    - 문단 전체에 적용된 요소 또는 요소를 담고 있는 컨테이너
    - 재사용 가능한 독립적 블록, 가장 바깥쪽 상위요소
    - 재사용을 위해 `margin`, `padding`을 적용하지 않음
2. Element
    - `.block__element`
    - block이 포함하고 있는 한 조각
    - 블록을 구성하는 종속적인 하위 요소
3. Modifier
    - `.block--modifier`
    - block 또는 element의 속성
``` css
<head>
<style>
    /* Block */
    .card {
      display: flex;
      flex-direction: column;
    }

    /* Element */
    .card__title {
      font-size: 2rem;
    }

    .card__list {
      margin: 0;
    }

    .card__button {
      font-size: 1rem;
      padding: 1rem;
      cursor: pointer;
    }

    /* Modifier */
    .card__list-item--none {
      list-style: none;
    }

    .card__button--red {
      background-color: crimson;
    }
  </style>
</head>
<body>
  <div class="card">
    <h2 class="card__title">제목</h2>
    <ul class="card__list">
      <li class="card__list-item--none">항목 1</li>
      <li class="card__list-item--none">항목 2</li>
    </ul>
    <button class="card__button card__button--red">버튼</button>
  </div>
</body>
```