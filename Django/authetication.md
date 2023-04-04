# Authentication System
```python
# settings.py
INSTALLED_APPS = [
    ...
    'django.contrib.auth',
]
```
- 사용자 인증과 관련된 기능을 모아 놓은 시스템
- 인증과 권한 부여를 함께 제공 및 처리
### 사전 설정
```
$ python manage.py startapp accounts
```
```python
# accounts/urls.py
from django.urls import path
from . import views

app_name='accounts'
urlpatterns = [

]
```
```python
# crud/urls.py
urlpatterns = [
    ...,
    path('accounts/', include('accounts.urls'))
]
```
<br>

## Custom User Model
- django가 제공하는 User Model은 수정할 수 없으므로 새로 만들어서 기본 모델로 지정해야 함
- 프로젝트 생성 후 바로 실행
  - 프로젝트 진행 중에 변경하게 되면 DB를 초기화하는 과정 필요
### 1. `AbstractUser`를 상속받는 커스텀 User 클래스 작성
- 기존 User 클래스도 `AbstractUser`를 상속받기 때문에 커스텀 User 클래스도 동일한 모습을 가짐
```python
# accounts/models.py
from django.contrib.auth.models import AbstractUser

class User(AbstractUser):
    pass # 아직은 수정할 게 없으므로 따로 작성하지 않음
```
### 2. 기본 User 모델을 커스텀 User 모델로 변경
```python
# settings.py
AUTH_USER_MODEL = 'accounts.User'
```
### 3. 모델 등록
```python
# accounts/admin.py
from django.contrib import admin
from django.contrib.auth.admin import UserAdmin
from .models import User

admin.site.register(User, UserAdmin)
```
<br>

## Login
- session을 create
### 1. 로그인 페이지
```python
# accounts/urls.py
app_name='accounts'
urlpatterns = [
    path('login/', view.login, name='login'),
]
```
```python
# accounts/views.py
from django.contrib.auth.forms import AuthenticationForm

def login(request):
    if request.method == 'POST'
        pass
    else:
        form = AuthenticationForm()

    context = {
        'form': form,
    }
    return render(request, 'accounts/login.html', context)
```
```html
<!-- accounts/login.html -->
<form action="{% url 'accounts:login' %}" method="POST">
  {% csrf_token %}
  {{ form.as_p }}
  <input type="submit">
</form>
```
### 2. 로그인 로직
```python
# accounts/views.py
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import login as auth_login
# view 함수 login과 이름이 같아서 별칭을 지정

def login(request):
    if request.method == 'POST'
        form = AuthenticationForm(request, request.POST)
        if form.is_valid():
            auth_login(request, form.get_user())
            return redirect('articles:index')
    else:
        form = AuthenticationForm()

    context = {
        'form': form,
    }
    return render(request, 'accounts/login.html', context)
```
<br>

## Logout
- session을 delete
```python
# accounts/urls.py
app_name='accounts'
urlpatterns = [
    path('login/', view.login, name='login'),
    path('logout/', view.logout, name='logout'),
]
```
```python
# accounts/views.py
from django.contrib.auth.forms import AuthenticationForm
from django.contrib.auth import logout as auth_logout

def logout(request):
    auth_logout(request)
    return redirect('articles:index')
```
```html
<!-- accounts/index.html -->
<a href="{% url 'accounts:login %}">login</a>
<form action="{% url 'accounts:logout' %}" method="POST">
  {% csrf_token %}
  <input type="submit" value="logout">
</form>
```

## Template with Authentication Data
### 현재 로그인 되어 있는 유저 정보 출력
```html
<!-- articles/index.html -->
<p>{{ user }}</p>
```
### 로그인 상태인지 판별
- `is_anonymous`: 로그아웃 상태면 True
- `is_authenticated`: 로그인 상태면 False
```html
<!-- articles/index.html -->
<!-- 로그인 상태면 로그아웃 버튼만 보이고, 로그아웃 상태면 로그인 버트만 보임 -->

{% if user.is_authenticated %}
  <form action="{% url 'accounts:logout' %}" method="POST">
  {% csrf_token %}
    <input type="submit" value="logout">
  </form>
{% else %}
  <a href="{% url 'accounts:login %}">login</a>
{% endif %}
```