# Pagination
- 데이터를 여러 페이지로 분할하여 보여주는 기능
## views.py
### 클래스 import
```python
from django.core.paginator import Paginator
```
### Paginator 인스턴스 생성
`Paginator(args1, args2)`
```python
article = Article.objects.all()
paginator = Paginator(article, 5)
```
- args1: 페이지를 나눠 보여질 전체 데이터(queryset, list 등)
- args2: 한 페이지에 보여질 데이터 수
### 현재 page 정보 받기
```python
page = request.GET.get('page', 1)
```
- url에서 page 정보를 가져옴
  - url에 page 값이 없으면 1
- http://(url)/articles/?page=2 인 경우 page 값은 2
### Page 인스턴스 생성
`get_page(args)`
```python
page_obj = paginator.get_page(page)
```
- get_page(args): 요청된 페이지(page)에 해당하는 데이터가 저장된 객체
- 전체 데이터가 아닌 해당 페이지의 데이터만 조회
### page_obj의 메소드
|메소드|설명|
|---|---|
|`count()`|전체 데이터 수|
|`get_page(number)`|number에 해당하는 페이지 가져오기|
|`page_range()`|페이지 범위|
|`number()`|현재 페이지 번호|
|`previous_page_number()`|이전 페이지 번호|
|`next_page_number()`|다음 페이지 번호|
|`has_previous()`|이전 페이지 존재 유무|
|`has_next()`|다음 페이지 존재 유무|
|`start_index()`|현재 페이지에 첫 번째로 저장된 데이터의 인덱스|
|`end_index()`|현재 페이지에 마지막으로 저장된 데이터의 인덱스|
```python
objects = ['item1', 'item2', 'item3', 'item4', 'item5', 'item6', 'item7']
paginator = Paginator(objects, 3)
page1 = paginator.page(1)
page2 = paginator.page(2)

print(paginator.page_range) # (1, 4)
print(page1.start_index()) # 1
print(page1.end_index()) # 3
print(page2.start_index()) # 4
print(page2.end_index()) # 6
```
### template에 넘겨주기
```python
context = {
    'articles': page_obj,
}
return render(request, 'articles/index.html', context)
```

<br>

## Template
- 부트스트랩에 있는 pagination 컴포넌트 활용
### 이전 / 다음 페이지 버튼
```html
<ul class="pagination justify-content-center">
  <!-- 이전 페이지가 있으면 활성화, 없으면 비활성화 -->
  {% if articles.has_previous %}
    <li class="page-item">
        <a class="page-link" href="?page={{ articles.previous_page_number }}">이전</a>
    </li>
  {% else %}
    <li class="page-item disabled">
        <a class="page-link" tabindex="-1" aria-disabled="true" href="#">이전</a>
    </li>
  {% endfor %}
  ...
  <!-- 다음 페이지가 있으면 활성화, 없으면 비활성화 -->
  {% if articles.has_previous %}
    <li class="page-item">
        <a class="page-link" href="?page={{ articles.previous_page_number }}">이전</a>
    </li>
  {% else %}
    <li class="page-item disabled">
        <a class="page-link" tabindex="-1" aria-disabled="true" href="#">이전</a>
    </li>
  {% endfor %}
</ul>
```
### 페이지 번호 리스트 생성
```html
<ul class="pagination justify-content-center">
  ...
  <!-- 페이지 범위만큼 반복 -->
  {% for page_num in articles.paginator.page_range %}
    <!-- 현재 페이지 기준 좌우로 5개씩만 보이도록 제한 -->
    {% if page_num >= articles.number|add:-5 and page_num <= articles.number|add:5 %}
      <!-- 현재 페이지 버튼 활성화 -->
      {% if page_num == articles.number %}
        <li class="page-item active" aria-current="page">
          <a class="page-link" href="?page={{ page_num }}">{{ page_num }}</a>
        </li>
      {% else %}
        <li class="page-item">
          <a class="page-link" href="?page={{ page_num }}">{{ page_num }}</a>
        </li>
      {% endif %}
    {% endif %}
  {% endfor %}
  ...
</ul>
```