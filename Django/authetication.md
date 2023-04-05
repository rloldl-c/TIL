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

## 로그인
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

## 로그아웃
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
<br>

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
<br>

## 회원가입
- user를 create
### 1. 회원가입 페이지 작성
```python
# accounts/urls.py
app_name='accounts'
urlpatterns = [
    ...,
    path('signup/', views.signup, name='signup'),
]
```
```python
# accounts/views.py
from django.contrib.auth.forms import UserCreationForm

def signup(request):
    if request.method == 'POST':
        pass
    else:
        form = UserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)
```
```html
<!-- accounts/signup.html -->
<form action="{% url 'accounts:signup' %}" method="POST">
  {% csrf_token %}
  <input type="submit" value="sign up">
</form>
```
### 2. 회원가입 로직
```python
# accounts/views.py

def signup(request):
    if request.method == 'POST':
        form = UserCreationForm(request.POST)
        if form.is_valid():
           form.save()
           return redirect('articles:index')
    else:
        form = UserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)
```
### `UserCreationForm()`
- 해당 폼에서 custom user model이 아닌 기존 user model을 사용하기 때문에 오류 발생
```python
# accounts/forms.py
# 현재 프로젝트에서 활성화된 사용자 모델을 반환
from django.contrib.auth import get_user_model
from django.contrib.auth.forms import UserCreationForm, UserChangeForm

class CustomUserCreationForm(UserCreationForm):
    class Meta(UserCreationForm.Meta):
        model = get_user_model()


class CustomUserChangeForm(UserChangeForm):
    class Meta(UserChangeForm.Meta):
        model = get_user_model()
```
### 수정된 회원가입 로직
```python
# accounts/views.py
from .forms import CustomUserCreationForm

def signup(request):
    if request.method == 'POST':
        form = CustomUserCreationForm(request.POST)
        if form.is_valid():
           form.save()
           return redirect('articles:index')
    else:
        form = CustomUserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)
```
<br>

## 회원 탈퇴
- user 객체를 delete
```python
# accounts/urls.py
app_name='accounts'
urlpatterns = [
    ...,
    path('delete/', views.delete, name='delete'),
]
```
```python
# accounts/views.py
from django.contrib.auth.forms import UserCreationForm

def delete(request):
    request.user.delete()
    return redirect('articles:index')
```
```html
<!-- articles/index.html -->
<form action="{% url 'accounts:delete' %}" method="POST">
  {% csrf_token %}
  <input type="submit" value="sign out">
</form>
```
### 탈퇴시 세션도 함께 지우기
```python
# accounts/views.py

def delete(request):
    request.user.delete()
    auth_logout(request)
    return redirect('articles:index')
```
- 탈퇴 후 로그아웃을 진행
- 로그아웃을 먼저 수행하면 탈퇴할 회원 정보가 없어짐
<br>

## 회원 정보 수정
```python
# accounts/urls.py
app_name='accounts'
urlpatterns = [
    ...,
    path('update/', views.update, name='update'),
]
```
```python
# accounts/views.py
from .forms import CustomUserChangeForm

def signup(request):
    if request.method == 'POST':
        pass
    else:
        form = CustomUserChangeForm(instance=request.user)
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)
```
```html
<!-- accounts/signup.html -->
<form action="{% url 'accounts:update' %}" method="POST">
  {% csrf_token %}
  {{ form.as_p }}
  <input type="submit">
</form>
```
### `CustomUserChangeForm` fields 재정의
- 재정의 하지 않을 경우 사용자가 admin 계정에서만 볼 수 있는 정보들도 수정이 가능
```python
# accounts/forms.py
class CustomUserChangeForm(UserChangeForm):
    class Meta(UserChangeForm.Meta):
        model = get_user_model()
        fields = ('email,' 'first_name', 'last_name')
```
### 수정된 로직
```python
# accounts/views.py

def signup(request):
    if request.method == 'POST':
        form = CustomUserChangeForm(request.POST, instance=request.user)
    else:
        form = CustomUserChangeForm(instance=request.user)
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)
```
<br>

## 비밀번호 변경
- `accounts/password/`
- django에서 정의한 비밀번호 변경 페이지가 존재
### 1. 비밀번호 변경 페이지 작성
```python
# accounts/urls.py
app_name='accounts'
urlpatterns = [
    ...,
    path('password/', views.change_password, name='change_password'),
]
```
```python
# accounts/views.py
from django.contrib.auth.forms import PasswordChangeForm

def signup(request):
    if request.method == 'POST':
        pass
    else:
        form = PasswordChangeForm(request.user)
    context = {
        'form': form,
    }
    return render(request, 'accounts/change_password.html', context)
```
```html
<!-- accounts/change_password.html -->
<form action="{% url 'accounts:change_password' %}" method="POST">
  {% csrf_token %}
  {{ form.as_p }}
  <input type="submit">
</form>
```
### 2. 비밀번호 변경 로직
```python
# accounts/views.py

def signup(request):
    if request.method == 'POST':
        form = PasswordChangeForm(request.user, request.POST)
        if form.is_valid():
           form.save()
           return redirect('articles:index')
    else:
        form = UserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)
```
### 세션 무효화
- 비밀번호가 변경되면 기존 세션과 일치하지 않아 로그아웃 상태로 redirect
```python
# accounts/views.py
from django.contrib.auth import update_session_auth_hash

def signup(request):
    if request.method == 'POST':
        form = PasswordChangeForm(request.user, request.POST)
        if form.is_valid():
           user = form.save()
           update_session_auth_hash(request, user)
           return redirect('articles:index')
    else:
        form = UserCreationForm()
    context = {
        'form': form,
    }
    return render(request, 'accounts/signup.html', context)
```