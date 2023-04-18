# 오늘 한 일
### 인스타그램 클론 코딩(미완)
### CSS - `::afetr`, `::before`
- `::after`: 선택한 요소 뒤에 삽입
- `::before`: 선택한 요소 앞에 삽입
``` css
.before::before {
  content: "before는 앞에 붙어요";
  color: red;
}
.after::after {
  content: "after는 뒤에 붙어요";
  color: blue;
}
```
``` html
<p class="before">
  before 예시
</p>
<!-- before는 앞에 붙어요  before 예시 -->
<p class="after">
  after 예시
</p>
<!-- after는 뒤에 붙어요 after 예시 -->
```
- `content`: 가짜요소, HTML문서에 포함되지 않은 요소를 CSS에서 새롭게 생성
    - `normal`: 기본값, `::before`나 `::after`와 함께 쓰일 경우 아무것도 생성하지 않음
    - `none`: 아무것도 생성하지 않음
    - `counter`: 카운터를 생성
    - `attr`(attribute): 지정한 속성(attribute)을 생성
        - `a` 태그 뒤에(`::after`) 괄호와 `href` 속성값을 출력
        ``` html
        <style>
          a::after {
            content: " (" attr(href) ")";
          }
        </style>
        ...
        <p>
        <a href="https://www.w3schools.com/css/">CSS Tutorial</a><br>
        <a href="https://www.w3schools.com/cssref/">CSS Reference</a>
        </p>

        <!-- CSS Tutorial(https://www.w3schools.com/css/) -->
        <!-- CSS Reference(https://www.w3schools.com/cssref/)-->
        ```
    - `string`: 지정한 문자열 생성
    - `url`: 지정한 미디어(이미지, 비디오 등) 생성