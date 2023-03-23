# DOM(Document Object Model)
- 문서(웹 페이지)를 객체로 제공
- 다른 프로그래밍 언어가 접근 가능
- DOM에서 모든 요소, 속성, 텍스트는 하나의 객체
    - 최상위 객체는 document
- 브라우저는 HTML 문서를 해석하여 DOM tree라는 객체의 트리로 구조화
### 웹 페이지를 조작하기 위한 순서
1. 조작하고자 하는 요소를 **선택**
2. 선택된 요소의 콘텐츠 또는 속성을 **조작**

<br>

## Query
### `document.querySelector(selectors)`
- 제공한 선택자와 일치하는 요소 하나 선택
- 제공한 선택자와 일치하는 첫 번째 요소 객체를 반환(없으면 null을 반환)
``` cs
// 클래스가 myclass인 첫 번째 요소 선택
const selector = document.querySelector('myclass');
```

### `document.querySelectorAll()`
- 제공한 선택자와 일치하는 모든 요소 선택
- 매칭할 하나 이상의 선택자를 인자(문자열)로 받음
- 제공한 선택자를 만족하는 NodeList를 반환
``` cs
// 모든 <p> 선택
const selector = document.querySelector('p');

// 클래스가 red와 small을 포함하는 모든 요소 선택
const selector = document.querySelector('.red.small');

// div의 요소 중에서 클래스가 note 또는 alter인 모든 요소 선택
const selector = document.querySelector('div.note, div.alert');
```

<br>

## Manipulation
### 1. attribute 조작
- `.classList.add(String)`
  - 지정한 클래스 값을 추가
  - 추가하려는 클래스가 요소에 이미 존재한다면 무시
- `.classList.remove(String)`
  - 지정한 클래스 값을 제거
- `.classList.item(Number)`
  - 인덱스로 접근하여 클래스 값을 반환
- `.classList.toggle(String, arg)`

``` html
<script>
  const h1Tag = document.querySelector('h1')

  // 위에서 지정한 h1 태그에 test 클래스를 추가
  h1Tag.classList.add('test')

  // 위에서 지정한 h1 태그에 test 클래스를 제거
  h1Tag.classList.remove('test')
</script>
```
- `.getAttribute(attrName)`
  - 해당 요소에 지정된 값을 반환
  - 존재하지 않는다면 null값이나 빈 문자열을 반환
- `.setAttribute(name, value)`
  - 지정한 요소로 속성 값을 설정
  - 속성이 이미 존재하면 입력된 값으로 업데이트, 없다면 새로운 속성으로 추가
- `.removeAttribute(attrName)`
  - 지정한 속성을 제거
``` html
<body>
  <a href="https://www.google.co.kr/?hl=ko">google</a>

  <script>
    const aTag = document.querySelector('a')

    console.log(aTag.getAttribute('href'))
    // https://www.google.co.kr/?hl=ko

    aTag.setAttribute('href', 'https://www.youtube.com/')
    // <a href="https://www.youtube.com/">google</a>

    aTag.removeAttribute('href')
    // <a>google</a>
  </script>
</body>
```

### 2. HTML 컨텐츠 조작
- `.textContent()` : 요소의 컨텐츠를 가져오거나 수정
``` html
<body>
  <div id="divA">This is <span>some</span> text!</div>

  <script>
    let text = document.querySelector('div').textContent;
    // text = 'This is some text!'

    document.querySelector('div').textContent = 'This text is different!';
    // <div id="divA">This text is different!</div>
  </script>
</body>
```

### 3. DOM 요소 조작
- `document.createElement(tagName)`
  - 지정한 요소를 새로 만듦
- `.appendChild(child)`
  - 지정한 요소를 부모 요소 마지막에 붙임
  - 주어진 요소가 부모에 이미 존재한다면, 현재 위치에서 새로운 위치로 이동
- `.removeChild(child)`
  - 지정한 요소를 제거하고 반환
``` html
<body>
  <div></div>

  <script>
    // 1. 태그 생성
    const h1Tag = document.createElement('h1')
    h1Tag.textContent = '제목'
    console.log(h1Tag)

    // 2-1. 추가할 부모를 선택
    const divTag = document.querySelector('div')

    // 2-2. 선택한 부모에 자식으로 추가
    divTag.appendChild(h1Tag)

    // 3. 삭제
    divTag.removeChild(h1Tag)
  </script>
</body>
```

### 4. 스타일 조작
```html
<body>
  <p>Heading</p>

  <script>
    const pTag = document.querySelector('p')
    pTag.style.color = 'red'
    pTag.style.fontSize = '36px'
  </script>
</body>
```