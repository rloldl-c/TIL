# Django design pattern
## Project
- project: 어플리케이션의 집합(DB 설정, URL 연결, 앱 전체 설정 등을 관리)
- application: 독립적으로 작동하는 기능 단위 모듈
    - 여러 앱이 하나의 프로젝트를 구성
<br>

## Design pattern
- 디자인 패턴: 소프트웨어 설계에서 발생하는 공통적인 문제를 해결하는 데 쓰이는 형식화된 관행

### MVC 디자인 패턴
- model - view - controller
- 데이터, 사용자 인터페이스, 비지니스 로직을 분리

### MTV 디자인 패턴
- model - template - view
- model: 응용프로그램의 데이터 구조를 정의하고 데이터베이스의 기록을 관리
- template: 화면상의 사용자 인터페이스 구조와 레이아웃을 정의
- view: model과 template 관련 로직을 처리해서 결과를 반환
- 기존 MVC 패턴의 명칭을 django에서 다르게 정의한 패턴

## Request & Response
- app 생성 및 등록 ➡ url.py ➡ view.py ➡ template 순서 
### 1. 앱 생성 및 등록
- 등록이 생성보다 선행되어서는 안됨
- 생성
``` python
# in terminal
python manage.py startapp app_name
```
- 등록
``` python
# in settings.py

INSTALLED_APPS = [
    'app_name',
    ...
]
```
### 2. `urls.py` 수정
``` python
# 1. app_name 폴더 내에 있는 views를 import
# 2. url 추가
from app_name import views

urlpatterns = [
    path('url/', views.func_name)
    # url/로 요청이 오면 views 모듈의 func_name 함수를 호출하겠다는 의미
]
```
### 3. `views.py`에 함수 추가
- 함수 인자로 전달되는 변수 **request** 이름 변경 불가
``` python
def func_name(request):
    return render(request, 'html_file_name')
```

### 4. 앱 폴더 내에 templates 폴더 생성 후 HTML 파일 추가
- **templates** 폴더 이름 변경 불가
- template 폴더에 하위 폴더를 만든다면 `views.py`에 경로를 추가해야 함
    ``` python
    def func_name(request):
        return render(request, 'folder_name/html_file_name')
    ```