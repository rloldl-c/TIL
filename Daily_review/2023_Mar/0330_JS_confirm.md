# 오늘 한 일
## JS - `confirm()`
- 메시지와 함께 알림 창을 띄우는 메서드
- 사용자가 'OK' 버튼을 누르면 `true`를 반환하고, 아니면 `false`를 반환
### Django에서 응용
```html
...
<a href="{% url 'app:delete' %}" onclick="return confirm('삭제하시겠습니까?');">삭제</a>
...
```
1. 링크를 누르면 '삭제하시겠습니까?' 메시지와 함께 confirm 창이 뜬다
2. 사용자가 'OK'를 누르면 delete url로 이동하여 삭제 로직을 실행한다
3. 사용자가 '취소'를 누르면 confirm 창이 닫히고 아무 일도 일어나지 않는다
