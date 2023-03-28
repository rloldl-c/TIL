# ORM(Object-Relational-Mapping)
- 객체 지향 프로그래밍 언어를 사용하여 호환되지 않는 유형의 시스템 간에 데이터를 변환하는 프로그래밍 기술
## QuerySet API
- ORM에서 데이터를 검색, 필터링, 정렬 및 그룹화 하는 데 사용하는 도구
- API를 사용하여 SQL이 아닌 파이썬 코드로 데이터를 처리
```python
# Model_class.Manager.QuerySetApi
Article.objects.all()
```
### Query
- 데이터베이스에 특정한 데이터를 보여 달라는 요청
- 쿼리문을 작성한다 == 원하는 데이터를 얻기 위해 데이터베이스에 요청을 보낼 코드를 작성한다
- 파이썬으로 작성한 코드가 ORM에 의해 SQL로 변환되어 데이터베이스에 전달되며, 데이터베이스의 응답을 ORM이 QuerySet이라는 자료 형태로 변환하여 우리에게 전달
### QuerySet
- 데이터베이스에게서 전달 받은 객체 목록(데이터 모음)
  - 순회가 가능한 데이터로써 1개 이상의 데이터를 불러와 사용할 수 있음
  - 단일 객체를 반환할 때는 QuerySet이 아닌 모델(class)의 인스턴스로 반환
- Django ORM을 통해 만들어진 자료형
<br>

## ORM Create
```
$ pip install ipython
$ pip install django-extensions
```
```python
# settings.py
INSTALLED_APPS = [
    'django_extensions',
    ...
]
```
### 데이터 객체를 만드는 방법
### 1. 인스턴스 변수에 각각 할당
```python
article = Article()
article.title = 'first'
article.content = 'django!'
# save()를 호출하지 않으면 DB에 저장되지 않음(레코드 생성 X)
article.save() 
```
### 2. 매개변수로 할당
```python
article = Article(title='second', content='django!')
article.save()
```
### `create()` 메서드 활용
```python
Article.objects.create(title='third', content='django!')
# save()를 따로 호출하지 않아도 저장
# 생성된 데이터 바로 반환
<Article: Article object(3)>
```
<br>

## ORM Read
## `all()`
- 전체 데이터 조회
```python
Article.objects.all()
<QuerySet [<Article: Article object (1)>, <Article: Article object (2)>, <Article: Article object (3)>]>
```

## `get()`
- 단일 데이터 조회
- 객체를 찾을 수 없으면 DoesNotExist 예외를 발생시키고, 둘 이상의 객체를 찾아도 MultipleObjectsReturned 예외를 발생시킴
- primary key와 같이 고유성을 보장하는 조회에서만 사용
```python
Article.objects.get(pk=1)
<Article: Article object (1)>
```

## `filter()`
- 특정 조건 데이터 조회
```python
Article.objects.filter(content='django!')
<QuerySet [<Article: Article object (1)>, <Article: Article object (2)>, <Article: Article object (3)>]>
```
### Field lookups
```python
# content에 dj가 포함된 모든 데이터 조회
Article.objects.filter(content__contains='dj')
```