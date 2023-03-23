# HTML
- HyperText Markup Language
- 웹 페이지의 의미와 구조를 정의하는 언어
- Hypertext: 웹 페이지를 다른 페이지로 연결하는 링크
- Markup Language: 태그 등을 이용하여 문서나 데이터의 구조를 명시하는 언어

## Structure
```html
<p class="editor-note"> Hello </p>
```
- 하나의 요소는 여는 태그와 닫는 태그, 그 안의 내용으로 구성
- 닫는 태그가 없는 태그도 존재
- 태그 속성
    - 요소 이름 바로 다음에 오는 속성은 요소 이름과 속성 사이에 공백으로 구분
    - 하나 이상의 속성들은 속성 사이에 공백으로 구분
    - 속성 값은 열고 닫는 따옴표로 지정
    - 나타내고 싶지 않지만 추가적인 기능, 내용을 담고 싶을 때 사용
    - CSS가 해당 요소를 선택하기 위한 값으로 활용

### 기본 구조
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>My page</title>
</head>
<body>
    <p>This is page</p>
</body>
</html>
```
- `<!DOCTYPE html>` : 해당 문서가 HTML 문서라는 것을 나타냄
- `<html></html>` : 전체 페이지의 콘텐츠를 포함
- `<title></title>` : 브라우저 탭 및 즐겨찾기 시 표시되는 제목
- `<head></head>` : 사용자에게 보이지 않는 HTML 문서에 관련된 설명이나 설정 등
- `<body></body>` : 페이지에 표시되는 모든 콘텐츠

<br>

## 텍스트 구조
1. Heading
- 제목 구분
- `<h1>`부터 `<h6>`까지 구분 가능
2. Paragraphs
- `<p>`로 문단을 구분
- 항상 새 줄에서 시작
- 브라우저가 문단 앞, 뒤에 공백(margin)을 추가
3. List
- `<ol>` : 순서가 있는 리스트
    - 사용 가능한 속성

        |속성명|속성값|설명|
        |---|---|---|
        |reverse|reversed|리스트 마커를 내림차순으로 변경|
        |start|숫자|리스트 마커의 시작값 변경|
        |type|1, A, a, I, i|리스트 아이템에 사용되는 마커 종류 변경|

- `<ul>` : 순서가 없는 리스트
- `<li>` : ol과 ul에 속하는 아이템을 나타낼 때 사용
    - ol에 속하는 아이템은 아라비아 숫자나 알파벳의 마커가 앞에 추가
    - ul에 속하는 아이템은 검정색 원이나 사각형 모양의 마커가 앞에 추가
4. Emphasis
- `<em>` : 기울임체
    - 구어체 강조와 같이 문장의 의미를 변경하는 데 사용
- `<strong>` : 볼드체
    - 문장의 일부분에 중요성을 추가하는 데 사용

<br>

# CSS
- Cascading Style Sheet
- 웹 페이지의 디자인과 레이아웃을 구성하는 언어
```css
h1{
    color: blue;
    font-size: 15px;
}
```
- `h1`: 선택자(selector)
- `color: blue` : 선언(declaration)
- `font-size` : 속성(property)
- `15px` : 값(value)

## 적용방법
1. 인라인(Inline) 스타일
```css
...
<body>
    <hl style="color: blue; background-color: yellow;">Hello World!</h1>
</body>
...
```
2. 내부(Internal) 스타일
```css
...
<style>
    h1 {
        color: blue;
        background-color: yellow;
    }
</style>
```
3. 외부(External) 스타일
- 별도의 CSS 파일 생성 후 불러오기
```css
<link rel="stylesheet" href="style.css">

/* style.css */
h1 {
    color: blue;
    background-color: yellow;
}
```

<br>

## Selector
- HTML 요소를 선택하여 스타일을 적용할 수 있도록 함
### 1. 기본 선택자
- 전체(*) 선택자
- 요소(tag) 선택자
    - 지정한 모든 태그를 선택
- 클래스(class) 선택자
    - 주어진 클래스 속성을 가진 모든 요소를 선택
    -  ex) `.index`는 `class="index"`를 가진 모든 요소 선택
- 아이디(id) 선택자
    - 주어진 아이디 속성을 가진 요소 선택
    - 문서에는 주어진 아이디를 가진 요소가 하나만 있어야 함
    - ex) `#index`는 `id="index"`를 가진 요소 선택
- 속성(attribute) 선택자
### 2. 결합자
- 자손 선택자(" ")
    - 첫 번째 요소의 자손 요소들 선택
    - ex) `p span`은 `<p>` 안에 있는 모든 `<span>`을 선택(하위 레벨 상관 X)
- 자식 선택자(">")
    - 첫 번째 요소의 직계 자식만 선택
    - ex) `ul > li`은 `<ul>` 안에 있는 모든 `<li>`를 선택(한 단계 아래 자식들만)