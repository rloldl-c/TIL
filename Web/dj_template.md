# Template
## DTL(Django Template Language)
- template에서 조건, 반복, 변수, 필터 등의 프로그래밍적 기능을 제공하는 시스템
### Variable
```
{{ variable}} 
```
- **view 함수**에서 render 함수의 세번째 인자로 딕셔너리 타입으로 넘겨 받을 수 있음
- 딕셔너리 key에 해당하는 문자열이 template에서 변수명으로 사용

### Filter
```
{{ variable|filter }}
```
- 표시할 변수를 수정할 때 사용

### Tag
```
{% tag %}
```
- 반복 또는 논리를 수행하여 제어 흐름을 만드는 등 변수보다 복잡한 일들을 수행
- 시작 태그와 종료 태그가 쌍을 이루는 태그도 존재

``` python
# views.py
def dinner(request):
    foods = ['볶음밥', '보쌈', '서브웨이', '햄버거',]
    picked = random.choice(foods)
    context = {
        'foods': foods,
        'picked': picked,
    }
    return render(request, 'articles/dinner.html', context)

```
``` html
<p>{{ picked }} 메뉴는 {{ picked|length }}글자 입니다.</p>

<h2>메뉴판</h2>
<ul>
  {% for food in foods %}
    <li>{{ food }}</li>
  {% endfor%}
</ul>

{% if foods|length == 0 %}
  <p>메뉴가 소진되었습니다.</p>
{% else %}
  <p>아직 메뉴가 남았습니다.</p>
{% endif %}
```
<br>

## 템플릿 상속
```
{ extends 'path' }
```
- 페이지의 공통 요소를 포함하고, 하위 템플릿이 재정의할 수 있는 공간을 정의
- 반드시 템플릿 최상위의 작성되어야 함
    - 2개 이상 상속 불가
``` html
<!-- 상속되는 상위 템플릿 base.html -->
<!DOCTYPE html>
<html lang="en">
  <head>
    ...
    {% block style %}
    {% endblock style %}
  </head>
  <body>
    {% block content %}
    {% endblock content %}
    ...
  </body>
</html>

<!-- 상속 받는 하위 템플릿 -->
{ extends 'base.html' }
{% block content %}
  ...
{% endblock content %}
```
<br>

## form을 통한 요쳥과 응답
### `form`
- 웹에서 사용자 정보를 입력하는 여러 방식을 제공
- 사용자로부터 할당된 데이터를 서버로 전송
- `action`: 입력 데이터가 전송될 URL
- `method`: 데이터를 어떤 방식으로 보낼 것인지 정의

### `input`
- 사용자의 데이터를 입력받을 수 있는 요소
- type 속성값에 따라 다양한 유형의 입력 데이터를 받음
- `name`: 서버가 사용자 입력 데이터에 접근할 수 있게 하는 속성

### `request`
- view 함수의 첫 번째 인자
- form에서 제출된 데이터가 저장된 객체
- `request.GET.get()`으로 form을 통해 제출된 데이터에 접근 가능

### 사용자가 입력한 데이터를 그대로 출력하는 프로그램
#### 1. 사용자가 데이터를 입력하는 화면 throw
``` python
# urls.py
urlpatterns = [
    path('throw/', views.throw),
]

# views.py
def throw(request):
    return render(request, 'throw.html')
```
``` html
<!-- throw.html -->
{% extends 'base.html' %}

{% block content %}
  <form action="/catch/" method="GET">
    <input type="text" class="form-control w-25 d-inline" name="content">
    <button type="submit" class="btn btn-primary">제출</button>
  </form>

{% endblock content %}
```
#### 2. 사용자가 입력한 데이터를 출력하는 화면 catch
``` python
# urls.py
urlpatterns = [
    path('catch/', views.catch),
]

# views.py
def catch(request):
    data = request.GET.get('content')

    context = {
        'data': data,
    }
    return render(request, 'catch.html', context)
```
``` html
<!-- catch.html -->
{% extends 'base.html' %}

{% block content %}
  <h1 class="fw-bold">{{ data }}</h1>
{% endblock content %}
```