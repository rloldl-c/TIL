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
from django.shortcuts import render, redirect

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

    # DB에 저장할 때는 페이지를 렌더링할 이유가 없음
    # return render(request, 'articles/create.html')
    return redirect('articles:detail', article.pk)
```
```html
<!-- templates/articles/new.html -->
<form action="{% url 'articles:create' %}" method="GET">
```
<br>

## HTTP Request method
### GET
- 특정 리소스를 조회할 때 사용
- `GET`으로 데이터를 전달하면 Query String 형식으로 전달

### POST
- 특정 리소스에 변경사항을 만드는 요청
- `POST`로 데이터를 전달하면 HTTP Body에 담겨서 전달
- url상에서 전달되는 내용이 보이지 않음

### CSRF token
- `csrf_token` 태그를 사용하지 않으면 403 Forbidden 에러 발생

<br>

## Delete
```python
# articles/urls.py
urlpatterns = [
    ...
    path('<int:pk>/delete/', views.delete, name='delete'),
]
```
``` python
# articles/views.py
def delete(request, pk):
    article = Article.objects.get(pk=pk)
    article.delete()
    return redirect('articles:index')
```
```html
<!-- templates/articles/detail.html -->
<form action="{% url 'articles:delete' article.pk %}" method="POST">
  <!-- a 태그를 사용하면 GET이 기본값이라 POST 메서드 사용 불가 -->
  {% csrf_token %}
  <input type="submit" value="삭제하기">
</form>
```

<br>

## Update
### 사용자의 입력을 받는 페이지 렌더링 함수 edit
```python
# articles/urls.py
urlpatterns = [
    ...
    path('<int:pk>/edit/', views.edit, name='edit'),
]
```
``` python
# articles/views.py
def edit(request, pk):
    article = Article.objects.get(pk=pk)
    context = {
        'article': article,
    }
    return render(request, 'articles/edit.html', context)
```
```html
<!-- templates/articles/edit.html -->
<body>
  <h1>Edit</h1>
  <form action="#" method="POST">
    {% csrf_token %}
    <div>
      <label for="title">제목</label>
      <!-- 수정 화면에서 이전 입력값이 보일 수 있도록 value를 지정 -->
      <input type="text" name="title" id="title" value="{{ article.title }}">
    </div>
    <div>
      <label for="content">내용</label>
      <textarea name="content" id="content" cols="30" rows="10">{{ article.content }}</textarea>
    </div>
    <input type="submit" value="수정하기">
    <a href="{% url 'articles:index' %}">뒤로가기</a>
  </form>
</body>
```
### 사용자가 입력한 데이터를 받아 DB에 저장하는 함수 update
```python
# articles/urls.py
urlpatterns = [
    ...
    path('<int:pk>/update/', views.update, name='update'),
]
```
``` python
# articles/views.py
def update(request, pk):
    title = request.POST.get('title')
    content = request.POST.get('content')
    article = Article.objects.get(pk=pk)
    article.title = title
    article.content = content
    article.save()

    return redirect('articles:detail', pk)
```
```html
<!-- templates/articles/edit.html -->
<body>
  <h1>Edit</h1>
  <form action="{% url 'articles:update' article.pk %}" method="POST">
...
</body>
```