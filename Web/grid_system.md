# Grid System
- 웹 페이지의 레이아웃을 조정하기 위해 사용하는 12개의 컬럼으로 구성된 시스템
- 반응형 디자인을 지원해 웹 페이지를 다양한 기기에서 적절하게 표시할 수 있도록 도움
- 각 요소가 12칸의 컬럼 중 몇 칸을 차지할 것인지를 지정
``` html
<div class="container">
  <div class="row">
    <div class"col-4"></div>
    <div class"col-4"></div>
    <div class"col-4"></div>
  </div>
</div>
```

### 중첩
```html
<div class="container">
  <div class="row">
    <div class"col-4"></div>
    <div class"col-8">
      <div class="row">
        <div class="col-6"></div>
        <div class="col-6"></div>
        <div class="col-6"></div>
        <div class="col-6"></div>
      </div>
    </div>
  </div>
</div>
```

### offset
- 요소 사이 공백
```html
<div class="container">
  <div class="row">
    <div class="box col-4">col</div>
      <div class="box col-4 offset-4">col</div>
    </div>
  <div class="row">
    <div class="box col-3 offset-3">col</div>
    <div class="box col-3 offset-3">col</div>
  </div>
  <div class="row">
    <div class="box col-6 offset-3">col</div>
  </div>
</div>
```

<br>

## Gutters
- column 사이에 있는 padding 영역
- Bootstrap의 padding과 margin spacer와 동일한 속성값을 가짐