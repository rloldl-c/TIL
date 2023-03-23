# URLs

## Variable Routing
- URL 일부에 변수를 포함시키는 것
- 변수는 view 함수의 인자로 전달 가능
``` python
# urls.py
path('articles/<int:num>/', views.detail)
path('hello/<str:name>/', views.greeting)
```
``` python
# views.py
def detail(request, num):
    context = {
        'num': num,
    }
    return render(request, 'articles/detail.html', context)


def greeting(request, name):
    context = {
        'name': name,
    }
    return render(request, 'articles/detail.html', context)
```
``` html
<!-- articles/detail.html -->
...
<p>{{ num }}번 글입니다</p>
...

<!-- hello/greeting.html -->
...
<p>{{ name }}님, 안녕하세요</p>
...
```
<br>

## App URL mapping
- 각 앱에 URL을 정의하는 것
- 프로젝트와 앱이 URL을 나누어 관리하여 주소 관리를 편하게 하기 위함
  - 앱이 여러 개일 경우 URL 중복을 방지할 수 있음
``` python
# in project urls.py
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    # url로 articles가 들어오면 articles.urls로 연결
    path('articles/', include('articles.urls')),
    path('pages/', include('pages.urls')) 
]
```
``` python
# articles/urls.py

from . import views

urlpatterns = [
    # articles/index
    path('index/', views.index),
    path('<int:num>', views.detail),
    path('greeting/<str:name>', views.greeting),
]
```
``` python
# pages/urls.py

from . import views

urlpatterns = [
    path('index/', views.index, name='index'),
]
```
<br>

## Naming URL pattern
- URL에 이름을 지정하는 것
- path 함수의 name 인자를 정의해서 사용
- `url` 태그로 절대 경로 주소 사용 가능
``` python
# articles/urls.py

urlpatterns = [
    path('index/', views.index, name='index'),
    path('<int:num>', views.detail, name='detail'),
    path('greeting/<str:name>', views.greeting, name='greeting'),
]
```
``` html
<!-- articles/index.html -->

{% block content %}
  <a href="{% url 'dinner' %}">dinner</a>
  <a href="{% url 'search' %'}">search</a>
  <a href="{% url 'throw' %}">throw</a>
  <a href="{% url 'index' %}">index</a>
{% endblock content %}
```
<br>

## URL Namespace
- `app_name`을 지정하여 다른 앱에서 이름이 겹칠 경우를 방지하기 위함
-  `url` 태그에서 url name 단독으로 사용 불가능
``` python
# articles/urls.py

app_name = 'articles'
urlpatterns = [
    path('index/', views.index, name='index'),
    path('<int:num>', views.detail, name='detail'),
    path('greeting/<str:name>', views.greeting, name='greeting'),
]
```
``` html
<!-- articles/index.html -->

{% block content %}
  <h1>Hello, {{ name }}!!</h1>
  <a href="{% url 'articles:dinner' %}">dinner</a>
  <a href="{% url 'articles:search' %}">search</a>
  <a href="{% url 'articles:throw' %}">throw</a>
  <a href="{% url 'articles:index' %}">index</a>
{% endblock content %}
...

```