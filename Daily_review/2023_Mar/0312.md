# 오늘 한 일
### 인스타그램 클론 코딩(미완)
### CSS - 미디어 쿼리
- 화면 크기에 따라 보여지는 스타일을 달라지게 함
- `@media`와 `@import` 등을 사용해 특정 조건에 따라 스타일을 적용
``` css
/* 화면(viewport) 너비가 12450px 이하인 경우에만 적용 */
@media (max-width: 12450px) { ... }

/* 화면 너비가 480px 이상 768px 이하인 경우에만 적용 */
@media screen and (min-width: 480px) and (max-width: 768px) { ... }
```
- `min-width`: 요소의 최소 너비 ➡ `min-width`로 설정된 값보다 **이상**인 경우에 적용되는 코드
- `max-width`: 요소의 최대 너비 ➡ `max-width`로 설정된 값보다 **이하**인 경우에 적용되는 코드
