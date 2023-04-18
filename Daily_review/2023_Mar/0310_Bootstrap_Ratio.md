# 오늘 한 일
### [Airbnb 클론 코딩 페어 프로젝트](/Exercise/Web/PJT/230310/airbnb.html)
### Bootstrap - Ratios
- 요소의 가로세로 비율을 설정
- 외부 콘텐츠 뿐만 아니라 `<div>`나 `<img>`에도 적용 가능
- 부모 요소에 적용하면 하위 요소에 적용
- aspect ratios
    ```html
    <div class="ratio ratio-1x1">
      <div>1x1</div>
    </div>
    <div class="ratio ratio-4x3">
      <div>4x3</div>
    </div>
    <div class="ratio ratio-16x9">
      <div>16x9</div>
    </div>
    <div class="ratio ratio-21x9">
      <div>21x9</div>
    </div>
    ```
- custom ratios
    ```html
    <!-- 2X1 비율 -->
    <div class="ratio" style="--bs-aspect-ratio: 50%;">
      <div>2x1</div>
    </div>
    ```