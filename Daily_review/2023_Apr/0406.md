# 오늘 한 일
## Algorithm
### 리스트 원형으로 순회하기
- 마지막 인덱스와 첫번째 인덱스를 함께 순회해야 하는 경우
```python
lst = [1, 2, 3, 4, 5]
list += list
```
<br>

## Django
### `{% url %}`에 variable 전달하기
- ex) navbar에서 메뉴에 따라 게시글 필터링 하기
```python
# accounts/urls.py
app_name='accounts'
urlpatterns = [
  ...,
    path('category/<str:subject>', views.category, name="category")
]
```
```python
# accounts/views.py
from .models import Post

def category(request, subject):
    posts = Post.objects.filter(category=subject)
    context = {
        'posts': posts,
    }
    return render(request, 'accounts/index.html', context)
```
```html
<!-- accounts/index.html -->
<a href="{% url 'accounts:category' '경제' %}">경제</a>
<a href="{% url 'accounts:category' '연예' %}">연예</a>
<a href="{% url 'accounts:category' '스포츠' %}">스포츠</a>
```
### 메뉴별 게시글 수 출력하기 - `count()`
```python
# accounts/views.py
from .models import Post

def category(request, subject):
    posts = Post.objects.filter(category=subject)
    economy_cnt = Post.objects.filter(category='경제').count()
    entrt_cnt = Post.objects.filter(category='연예').count()
    sports_cnt = Post.objects.filter(category='스포츠').count()
    context = {
        'posts': posts,
        'economy_cnt': economy_cnt,
        'entrt_cnt': entrt_cnt,
        'sports_cnt': sports_cnt,
    }
    return render(request, 'accounts/index.html', context)
```
```html
<!-- accounts/index.html -->
<a href="{% url 'accounts:category' '경제' %}">경제({{ economy_cnt }}})</a>
<a href="{% url 'accounts:category' '연예' %}">연예({{ entrt_cnt }}})</a>
<a href="{% url 'accounts:category' '스포츠' %}">스포츠({{ sports_cnt }}})</a>
```