# Positioning
- Normal Flow에서 요소를 끄집어 내서 다른 위치로 배치하는 것
### 1. static
- 기본값
- 요소를 normal flow에 따라 배치
### 2. relative
- 요소를 normal flow에 따라 배치
- 자신의 static값을 기준으로 이동
- 요소가 차지하는 공간이 static일 때와 같음
```css
.container {
    position: relative;
    top: 10px;
} 
/* 원래 위치에서 10px 아래에 배치 */
```
### 3. absolute
- 요소를 normal flow에서 제거
- 가장 가까운 relative 요소를 기준으로 이동
- 요소가 차지하는 공간이 없어짐
    - 해당 요소보다 아래에 작성된 요소들의 위치도 변경(요소가 차지하는 공간이 없어져서 아래에 배치된 요소가 위로 올라오는 등)
    - 다른 요소와 겹치게 배치 가능

### 4. fixed
- 요소를 normal flow에서 제거
- 현재 화면 영역(viewport)를 기준으로 이동
- 요소가 차지하는 공간이 없어짐
    - 다른 요소와 겹치게 배치 가능
- 스크롤을 해도 위치가 변하지 않음

### 5. sticky
- 요소를 normal flow에 따라 배치
- 가장 가까운 block 요소를 기준으로 이동
- 요소가 특정 임계점에 스크롤 될 때 그 위치에 고정(fixed)
- 다음 sticky 요소가 임계점에 도달하면 이전 요소의 자리를 대체

<br>

## z-index
- static 외의 position 요소 박스에 적용
- 정수 값을 사용해 Z축 순서를 지정
- 더 큰 값을 가진 요소가 작은 값의 요소를 덮음
```css
z-index: -1;
/* 음수값으로 우선순위를 낮출 수 있음 */
```