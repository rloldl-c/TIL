# 오늘 한 일
## CSS
### `:first-child`
- 자식 요소 중 첫 요소를 선택
- 전체 자식 요소 중에서 가장 첫 번째에 위치해야 선택 가능
  - 위에 다른 요소가 있으면 첫 번째가 아니기 때문에 선택되지 않음
```css
.parent .child:first-child {
  color: red;
}
```
```html
<div class="parent">
  <!-- first가 적힌 p 태그에 적용 -->
  <p class="child">first</p>
  <p class="child">second</p>
  <p class="child">third</p>
</div>
```
```html
<div class="parent">
  <!-- css가 적용되지 않음 -->
  <h1>title</h1>
  <p class="child">first</p>
  <p class="child">second</p>
  <p class="child">third</p>
</div>
```

<br>

### `:first-of-type`
- 자식 요소 중 현재 요소와 일치하는 첫 요소를 선택
- 동일한 태그나 클래스 중에서 첫 요소기 때문에 위에 다른 요소가 있어도 선택 가능
```css
.parent .child:first-of-type {
  color: red;
}
```
```html
<div class="parent">
  <!-- first가 적힌 p 태그에 적용 -->
  <p class="child">first</p>
  <p class="child">second</p>
  <p class="child">third</p>
</div>
```
```html
<div class="parent">
  <!-- first가 적힌 p 태그에 적용 -->
  <h1>title</h1>
  <p class="child">first</p>
  <p class="child">second</p>
  <p class="child">third</p>
</div>
```