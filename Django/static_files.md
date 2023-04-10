# Static files
## 경로에 따른 static file 제공하기
### 1. 기본 경로
### `app/static/`
- articles/static/articles/ 경로에 이미지 파일 저장
- static tag를 사용해 이미지 파일에 대한 url 제공
```html
<!-- articles/index.html -->
{% load static%}
<img src="{% static 'articles/sample-1.png' %}" alt="">
```

### 2. 추가 경로
### `STATICFILES_DIRS`
- STATIC_URL: 기본 경로 및 추가 경로에 위치한 정적 파일을 참조하기 위한 URL
``` python
# articles/settings.py
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    BASE_DIR / 'static',
]
```
- static/ 경로에 이미지 파일 저장
- static tag를 사용해 이미지 파일에 대한 url 제공
```html
<!-- articles/index.html -->
{% load static%}
<img src="{% static 'sample-2.png' %}" alt="">
```
<br>

## Media Files
- 사용자가 웹에 업로드하는 정적 파일
### 1. settings.py에 MEDIA_ROOT, MEDIA_URL 설정
```python
# articles/settings.py
MEDIA_ROOT = BASE_DIR / 'media'
MEDIA_URL = '/media/'
```
### 2. MEDIA_ROOT와 MEDIA_URL에 대한 url 설정
```python
# pjt/urls.py
from django.conf import settings
from django.conf.urls.static import static
urlpatterns = [
    ...
] + static(settings.MEDIA_URL, documents_root=settings.MEDIA_ROOT)
```
- 업로드된 파일의 URL => settings.MEDIA_URL
- 파일의 실제 위치 => settings.MEDIA_ROOT
<br>

## 이미지 업로드
### 1. 이미지 모델 필드 추가
```python
# articles/models.py
class Article(models.Model):
    ...,
    image = models.ImageField(blank=True, upload_to='images'),
```
- ImageField() : 이미지 업로드에 사용하는 모델 필드
  -   이미지 객체가 직접 저장되는 게 아닌 '이미지 파일 경로의 문자열'이 저장
- upload_to : 미디어 파일 추가 경로 설정
### 2. migration 진행
```
$ pip install pillow

$ python manage.py makemigraions
$ python manage.py migrate

$ pip freeze > requirements.txt
```
### 3. form 속성에 enctype 속성 추가
```html
<!-- articles/create.html -->
<form action="{% url 'articles:create' %}" method="POST" enctype="multipart/form-data">
  ...
</form>
```
### 4. views 함수에 파일 업로드에 대한 코드 추가
```python
# articles/views.py
def create(request):
    if request.method == 'POST':
        form = ArticleForm(request.POST, request.FILES)
        ...
```
<br>

## 이미지 제공
```html
<img src="{{ article.image.url }}" alt="">
```
- 이미지를 업로드 하지 않은 게시물이 존재하는 경우
```html
{% if article.image %}
  <img src="{{ article.image.url }}" alt="">
<!-- default 이미지를 지정하는 방법도 있음
{% else%}
  <img src="{% static 'no_image.png' %}" alt=""> -->
{% enif%}
```
<br>

## 업로드한 이미지 수정
### 1. 수정 페이지 form 요소에 enctype 속성 추가
```html
<!-- articles/update.html -->
<form action="{% url 'articles:update' article.pk %}" method="POST" enctype="multipart/form-data">
  ...
</form>
```
### 2. view 함수에서 이미지 수정에 대한 코드 추가
```python
# articles/views.py
def update(request, pk):
    article = Article.objects.get(pk-pk)
    if request.method == 'POST':
        form = ArticleForm(request.POST, request.FILES, instance=article)
        ...
```