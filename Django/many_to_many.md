# Many to many relationships
## N:1의 한계
### 1. N:1 모델 관계 설정
- 한 명의 의사에게 여러 환자가 예약할 수 있다고 설정
```python
class Doctor(models.Model):
    name = models.TextField()

class Patient(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    name = models.TextField()
```
- 각각 2명의 의사와 환자를 생성하고 환자는 서로 다른 의사에게 예약을 한 상황
```python
doctor1 = Doctor.objects.create(name='alice')
doctor2 = Doctor.objects.create(name='bella')
patient1 = Patient.objects.create(name='carol', doctor=doctor1)
patient2 = Patient.objects.create(name='dane', doctor=doctor2)
```
- 이 상황에서 1번 환자(carol)가 2번 의사(bella)는 예약할 수 있는 방법은?
  - 동일한 환자를 새로운 patient 객체로 추가
  - 예약 테이블을 따로 생성

### 2. 중개 모델(예약 테이블)
```python
# 외래키 삭제
class Patient(models.Model):
    name = models.TextField()

# 중개모델 작성
class Reservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
```
- 중개 모델에는 id, patient_id, doctor_id 필드만 존재
- Reservation 모델은 의사와 환자에 각각 N:1 관계를 가짐
```python
doctor1 = Doctor.objects.create(name='alice')
patient1 = Patient.objects.create(name='carol')

Reservation.objects.create(doctor=doctor1, patient=patient1)

patient2 = Patient.objects.create(name='dane')

Reservation.objects.create(doctor=doctor1, patient=patient2)
```
- patient 객체를 추가하지 않아도 의사 모두에게 예약 가능

### 3. ManyToManyField 작성
```python
class Patient(models.Model):
    # ManyToManyField 작성
    doctors = models.ManyToManyField(Doctor)
    name = models.TextField()

# Reservation Class 주석 처리
```
### 4. `through` argument
- 중개 모델을 수동으로 지정하려는 경우 사용하는 옵션
- 추가 데이터를 사용하여 다대다 관계와 연결하려는 경우 사용
```python
class Patient(models.Model):
    doctors = models.ManyToManyField(Doctor, through='Reservation')
    name = models.TextField()


class Reservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
    symptom = models.TextField()
    reserved_at = models.DateTimeField(auto_now_add=True)
```
- 증상과 예약일을 추가하여 예약 저장 가능

<br>

## ManyToManyField
### `related_name`
- 역참조시 사용하는 manager name 변경
```python
class Patient(models.Model):
    # ManyToManyField - related_name 작성
    doctors = models.ManyToManyField(Doctor, related_name='patients')
    name = models.TextField()
```
```python
# related_name 지정 전
doctor.patient_set.all()

# related_name 지정 후
doctor.patients.all()
```
### `through`
- 중개 모델을 직접 작성하는 경우 사용
- 중개 모델에 추가적인 데이터를 사용하는 경우
### `symmetrical`
- ManyToManyField가 동일한 모델을 가리키는 정의에서만 사용
```python
class Person(models.Model):
    friends = models.ManyToManyField('self', symmetrical=True)
```
- _set 매니저를 추가하지 않음
- source 모델의 인스턴스가 target 모델의 인스턴스를 참조할 때 자동으로 target 모델의 인스턴스도 source 모델의 인스턴스를 참조
- ex) SNS에서 내가 상대방을 팔로우하면 자동으로 상대방도 나를 팔로우하게 됨

<br>

## Article-User
- '좋아요' 기능 추가해보기
### 1. 모델 설정
```python
# articles/models.py
class Article(models.Model):
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    like_users = models.ManyToManyField(settings.AUTH_USER_MODEL),
    ...
```
#### migration 진행시 오류 발생
- like_users 필드에서 역참조를 진행할 시 .article_set 매니저가 생성
- 이 매니저는 이전 필드 매니저(user.article_set) 이름과 충돌
- related_named을 작성해서 충돌 해결
```python
# articles/models.py
class Article(models.Model):
    user = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    like_users = models.ManyToManyField(settings.AUTH_USER_MODEL, related_name='like_articles'),
    ...
```
#### 현재 모델에서 사용 가능한 related manager 정리
1. article.user: 게시글을 작성한 유저
2. user.article_set: 유저가 작성한 게시글(역참조)
3. article.like_users: 게시글을 좋아요한 유저
4. user.like_articles: 유저가 좋아요한 게시글(역참조)

<br>

### 2. 좋아요 기능 구현
```python
# articles/urls.py

urlpatterns = [
    ...,
    path('<int:article_pk>/likes/', views.likes, name='likes'),
]
```
```python
# articles/views.py

def likes(request, article_pk):
    article = Article.objects.get(pk=article_pk)

    if request.user in article.like_users.all():
        article.like_users.remove(request.user)
    else:
        article.like_users.add(request.user)
    return redirect('articles:index')
```
```html
<!-- articles/index.html -->
{% for article in articles %}
  ...
  <form action="{% url 'articles:likes' article.pk %}" method="POST">
    {% csrf_token %}
    {% if request.user in article.like_users.all %}
      <input type="submit" value="취소">
    {% else %}
      <input type="submit" value="좋아요">
    {% endif %}
  </form>
  <hr>
{% endfor %}
```