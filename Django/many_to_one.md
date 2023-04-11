# Many to one relationship
- 한 테이블의 0개 이상의 레코드가 다른 테이블의 레코드 한 개와 관련된 관계
  - 0개 이상의 댓글은 하나의 게시글에 작성될 수 있음
```python
# articles/models.py
class Comment(models.Model):
    article = models.ForeignKey(Article, on_delete=models.CASCADE)
    content = models.CharField(max_length=200)
    ...
```
### `ForeignKey(to, on_delete)`
- django에서 N:1 관계 설정 모델 필드
- to: 참조하는 모델 class 이름
- on_delete: 참조하는 모델 class가 삭제될 경우, 연결된 하위 객체의 동작을 결정
  - `CASCADE`, `PROTECT`, `SET_NULL` 등
  - https://docs.djangoproject.com/en/3.2/ref/models/fields/#arguments
- migration 후 ForeignKey 필드는 `article_id`로 생성

<br>

## 역참조
- N:1 관계에서 1이 N을 참조하는 상황
### related manager `article.comment_set.all()`
- 역참조시 사용하는 manger
- Article 클래스에는 Comment 관계에 대해 작성한 것이 없으므로 django에서 제공하는 manger를 통해 Comment 객체를 참조

<br>

## 댓글 입력 받기
### 1. CommentForm 작성
```python
# articles/forms.py
class CommentForm(forms.ModelForm):
    class Meta:
        model = Comment
        fields = ('content',)
```
- 모든 필드를 출력하면 사용자의 입력이 필요 없는 foreign key에 대한 form도 출력됨
- 사용자의 입력이 필요한 필드만 출력되도록 작성
### 2. CommentForm 출력
```python
# articles/views.py
def detail(request, pk):
    article = Article.objects.get(pk=pk)
    comment_form = CommentForm()
    context = {
      'article': article,
      'comment_form': comment_form,
    }
    return render(request, 'articles/detail.html', context)
```
```html
<!-- articles/detail.html -->
<form action="" method="POST">
  {% csrf_token %}
  {{ comment_form }}
  <input type="submit">
</form>
```
### 3. foreign key 받기
- detail url에 사용된 게시글의 pk값을 사용
- comment.article_id = article.pk 처럼 pk 값을 직접 입력하는 방법은 권장하지 않음
```python
# articles/urls.py
urlpatterns = [
    ...,
    path('<int:pk>/comments/', views.comments_create, name='comments_create'),
]
```
```python
# articles/views.py
def comments_create(request, pk):
    article = Article.objects.get(pk=pk)
    comment_form = CommentForm()
    if comment_form.is_valid():
      comment = comment_form.save(commit=False)
      comment.article = article
      comment_form.save()
      return redirect('articles:detail', article.pk)
    context = {
        'article': article,
        'comment_form': comment_form,
    }
    return render(request, 'articles/detail.html', context)
```
```html
<!-- articles/index.html -->
<form action="{% url 'articles:comment_create' article.pk %}" method="POST">
  {% csrf_token %}
  {{ comment_form }}
  <input type="submit">
</form>
```

<br>

## 댓글 출력하기
```python
# articles/views.py
def detail(request, pk):
    article = Article.objects.get(pk=pk)
    comment_form = CommentForm()
    comments = article.comment_set.all()
    context = {
      'article': article,
      'comment_form': comment_form,
      'comments': comments,
    }
    return render(request, 'articles/detail.html', context)
```
```html
<!-- articles/detail.html -->
<ul>
  {% for comment in comments %}
    <li>{{ comment.content }}</li>
  {% endfor%}
</ul>
```

<br>

## 댓글 삭제하기
```python
# articles/urls.py
urlpatterns = [
    ...,
    path('<int:article_pk>/comments/<int:comment_pk>/delete/', views.comments_delete, name='comments_delete'),
]
```
```python
# articles/views.py
def comments_delete(request, article_pk, comment_pk):
    comment = Comment.objects.get(pk=comment_pk)
    comment.delete()
    return redirect('articles:detail', article_pk)
```
```html
<!-- articles/detail.html -->
<ul>
  {% for comment in comments %}
    <li>
      {{ comment.content }}
      <form action="{% url 'articles:comments_delete' article.pk comment.pk%}" method="POST">
        <input type="submit">
      </form>
    </li>
  {% endfor%}
</ul>
```