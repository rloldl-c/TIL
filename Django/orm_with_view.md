# ORM with view
## Read
### 전체 게시글 조회
- 글 제목을 누르면 해당 글 상세 페이지로 이동
```python
# article/views.py
from .models import views

def index(request):
    articles = Article.objects.all()
    context = {
        'articles': articles,
    }
    return render(request, 'articles/index.html', context)
```
```html
<!-- articles/index.html -->
{% for article in articles%}
  <p>글 번호: <a href="{% url 'articles:detail' article.pk %}">{{ article.pk }}</p>
  <p>글 제목: {{ article.title }}</p>
  <p>글 내용: {{ article.content }}</p>
{% endfor %}
```
<br>

### 단일 게시글 조회
```python
# articles/urls.py
urlpatterns = [
    path('<int:pk>/', views.detail, name='detail'),
]
```
```python
# article/views.py
from .models import views

def details(request, pk):
    article = Articles.objects.get(pk=pk)
    context = {
        'article': article,
    }
    return render(request, 'articles/detail.html', context)
```
```html
<!-- templates/articles/index.html -->
<h3>{{ article.pk }}번째 글</h3>
<p>제목: {{ article.title }}</p>
<p>내용: {{ article.content }}</p>
<p>작성 시각: {{ article.created_at }}</p>
<p>수정 시각: {{ article.updated_at }}</p>
<a href="{% url 'articles:index' %}">뒤로가기</a>
```
<br>

## Create
### 사용자의 입력을 받는 페이지 렌더링 함수 new
```python
# articles/urls.py
urlpatters = [
  path('new/', views.new, name='new'),
]
```
```python
# articles/views.py
def new(request):
    return render(request, 'articles/new.html')
```
```html
<!-- templates/articles/new.html -->
<form action="#" method="GET">
    <div>
      <label for="title">제목</label>
      <input type="text" name="title" id="title">
    </div>
    <div>
      <label for="content">내용</label>
      <textarea name="content" id="content" cols="30" rows="10"></textarea>
    </div>
    <input type="submit">
    <a href="{% url 'articles:index' %}">뒤로가기</a>
  </form>
```
### 사용자가 입력한 데이터를 받아 DB에 저장하는 create 함수
```python
# articles/urls.py
urlpatters = [
  path('create/', views.create, name='create'),
]
```
```python
# articles/views.py
def create(request):
    title = request.GET.get('title')
    content = request.GET.get('content')
    # article = Articles()
    # article.title = title
    # article.content = content
    # article.save()

    # save 전에 유효성 검사 등의 작업을 진행할 수 있어서 이 방법을 사용
    article = Articles(title=title, content=content)
    article.save()

    # Articles.objects.create(title=title,content=content)
    return render(request, 'articles/create.html')
```
```html
<!-- templates/articles/new.html -->
<form action="{% url 'articles:create' %}" method="GET">
```