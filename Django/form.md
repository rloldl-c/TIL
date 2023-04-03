# Form
## Django Form
- 사용자 입력 데이터를 수집하고, 처리 및 유효성 검증을 수행하기 위한 도구
### Form class 선언
``` python
# articles/forms.py
from django import forms

class ArticleForm(forms.Form):
    title = forms.CharField(max_length=10)
    content = forms.CharField()
```
### Form class를 이용한 입력 template
```python
# articles/views.py
from .forms import ArticleForm

def new(request):
    form = ArticleForm()
    context = {
        'form': form,
    }
    return redner(request, 'articles/new.html', context)
```
```html
<!-- articles/new.html -->
<h1>New</h1>
<form action="{% url 'articles:create' %}" method="POST">
  {% csrf_token %}
  {{ form.as_p }}
  <input type="submit">
</form>
```
<br>

## Widgets
- HTML 'input' element의 표현을 담당
- input 요소의 속성 및 출력되는 부분을 변경
### widget으로 속성값 추가하기
```python
articles/forms.py
from django import forms

class ArticleForm(forms.Form):
    title = forms.CharField(
        label='제목',
        widget=forms.TextInput(
            attrs={
                'class': 'my-title',
                'placeholder': 'Enter the title',
                'maxlength': 10,
            }
        )
    )
    content = forms.CharField()
```
<br>

## Django ModelForm
- form: 사용자 입력 데이터를 저장하지 않을 때
- modelform: 사용자 입력 데이터를 DB에 저장해야 할 때
### ModelForm 선언
```python
# articles/forms.py
from django import forms
from .models import Article

class ArticleForm(forms.ModelForm):
    class Meta:
        model = Article
        fields = '__all__' # 모든 필드를 입력 받음
        fields = ('title', ) # title 속성만 입력 받음
        exclude = ('title', ) # title을 제외하고 모두 입력 받음
```

### ModelForm을 이용한 입력 데이터 저장 로직
```python
# articles/views.py
from .forms import ArticleForm

def create(request):
    form = ArticleForm(request.POST)
    
    if form.is_valid(): #유효성 검사를 통과한 input만 저장
        article = form.save()
        return redirect('articles:detail', article.pk)
    
    context = {
        'form': form,
    }
    return render(request, 'articles/new.html', context)
```
### ModelForm을 이용한 입력 데이터 수정 로직
```python
# articles/views.py

def update(request, pk):
    article = Article.objects.get(pk=pk)
    # 원본 데이터 article을 form의 두번째 인자로 넘겨줘서 어느 부분을 수정할지 판단
    form = ArticleForm(request.POST, instance=article)

    if form.is_valid():
        form.save()
        return redirect('articles:detail', article.pk)

    context = {
        'form': form,
    }
    return render(request, 'articles/edit.html', context)
```
<br>

# Handling HTTP requests
## HTTP request에 따른 view 함수 구조 변화
### 새로 입력 받은 데이터를 저장할 때 별도의 view 함수를 구현하지 않아도 됨
- request의 method에 따라 처리 방식을 나눠줌
- GET: 입력 받는 폼을 반환
- POST: 입력 받은 데이터를 저장
```python
def create(request):
    if request.method == 'POST':
        form = ArticleForm(request.POST)
        if form.is_valid():
            article = form.save()
            return redirect('articles:detail', article.pk) # 새로 생성한 article 페이지 반환
    else: # method == 'GET'
        form = ArticleForm()

    context = {
        'form': form,
    }
    return render(request, 'articles/new.html', context) # 입력 폼이 있는 페이지 반환
```