# Model
- DB의 테이블을 정의하고 데이터를 조작할 수 있는 기능들을 제공
- 테이블 구조를 설계하는 청사진

<br>

## model 클래스 작성
``` python
# todos/models.py

class Todo(models.Model):
    content = models.CharField(max_length=80)
    completed = models.BooleanField(default=False)
    priority = models.IntegerField(default=3)
```
- id 필드는 자동 생성
- `django.db.models` 모듈의 `Model`이라는 부모 클래스를 상속 받아 작성
- model 기능에 관련된 모든 설정이 담긴 클래스
- 클래스의 변수로 테이블의 필드 생성
- model의 `Field` 메서드로 테이블 필드의 데이터 타입을 지정
- `Field` 메서드의 키워드 인자로 테이블 필드의 제약조건을 설정

<br>

## Migrations
- model 클래스의 변경사항(필드 생성, 수정 등)을 DB에 최종 반영하는 방법
#### 1. model 클래스를 기반으로 설계도 작성
```
$ python manage.py makemigrations
```
#### 2. 만들어진 설계도를 DB에 전달하여 반영
```
$ python manage.py migrate
```
<br>

### 이미 생성한 테이블에 필드 추가하기
``` python
# todos/models.py

class Todo(models.Model):
    content = models.CharField(max_length=80)
    completed = models.BooleanField(default=False)
    priority = models.IntegerField(default=3)
    created_at = models.DateField(auto_now_add=True) # 추가한 필드
    deadline = models.DateField(null=True) # 추가한 필드
```
```
$ python manage.py makemigrations

You are trying to add a non-nullable field 'category' to todo without a default; we can't do that (the database needs something to populate existing rows).
Please select a fix:
 1) Provide a one-off default now (will be set on all existing rows 
with a null value for this column)
 2) Quit, and let me add a default in models.py
Select an option:
```
- 이미 기존 테이블이 존재하기 때문에 새로 추가된 필드에 기본값이 필요
1) 현재 창에서 기본값을 직접 입력
2) 현재 창을 나가고 models.py에 기본값을 설정

<br>

## Admin site
### 관리자 계정 만들기
```
$ python manage.py createsuperuser
```
- DB에 생성한 관리자 계정이 있는지 확인
### 모델 클래스 등록
``` python
# todos/admin.py
from .models import Todo

admin.site.register(Todo)
```
- 등록하지 않으면 admin site에서 확인 불가능