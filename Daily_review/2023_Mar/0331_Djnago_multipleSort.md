# 오늘 한 일
## 가계부 서비스 개발
## Django - 조회 기준(or 정렬) 여러 개 설정하기
- 설정1. 입력 순서, 사용 금액, 날짜에 따라 정렬
- 설정2. 선택한 카테고리에 맞는 항목만을 조회
### 1. 조회할 항목을 `form` 안에 `select` 태그로 만들기
- 항목이 여러 개라면 `select`를 여러 개 만들어야 함
``` html
<!-- index.html -->

<form method="GET">
  {% comment %} 정렬 {% endcomment %}
  <div class="mb-3">
    <label for="sort" class="form-label">정렬 기준</label>
    <select class="w-50 form-select" id="sort" name="sort">
      <option selected>정렬 기준 선택</option>
      <option {% if sort == 'pk' %}selected{% endif %} value="pk">입력 순서(오래된순)</option>
      <option {% if sort == 'pk_desc' %}selected{% endif %} value="pk_desc">입력 순서(최신순)</option>
      <option {% if sort == 'amount' %}selected{% endif %} value="amount">사용 금액(오름차순)</option>
      <option {% if sort == 'amount_desc' %}selected{% endif %} value="amount_desc">사용 금액(내림차순)</option>
      <option {% if sort == 'date_desc' %}selected{% endif %} value="date_desc">사용 날짜(최신순)</option>
      <option {% if sort == 'date' %}selected{% endif %} value="date">사용 날짜(오래된순)</option>
    </select>
  </div>
  {% comment %} 조회 {% endcomment %}
  <div class="mb-3">
    <label for="choice" class="form-label">분류</label>
    <select class="w-50 form-select" id="choice" name="choice">
      <option selected>카테고리 선택</option>
      <option value="all">전체</option>
      <option {% if choice == '식비' %}selected{% endif %} value="식비">식비</option>
      <option {% if choice == '카페' %}selected{% endif %} value="카페">카페</option>
      <option {% if choice == '교통비' %}selected{% endif %} value="교통비">교통비</option>
      <option {% if choice == '문화생활' %}selected{% endif %} value="문화생활">문화생활</option>
      <option {% if choice == '의류' %}selected{% endif %} value="의류">의류</option>
    </select>
  </div>
  <input type="submit" class="btn btn-outline-secondary" value="적용">
</form>
```
<br>

### 2. `views.py`에 함수 작성
#### 2-1. 조회할 항목이 넘어오면 그 항목을 변수에 할당
- 딕셔너리의 `get()` 메서드로 값이 넘어오지 않을 때에 에러가 발생하지 않도록 기본값을 지정
```python
def index(request):
  choice = request.GET.get('choice',' ')
  sort = request.GET.get('sort', ' ')
  
  return render(request, 'abs/index.html')
```
#### 2-2. 넘어온 항목에 맞춰 조회 기준 생성
- 페이지를 렌더링 하는 함수가 아닌 파이썬 함수로 생각하기
``` python
def index(request):
  abs = AccountBook.objects.all()
  choice = request.GET.get('choice',' ')
  abs = choice_category(abs, choice)
  sort = request.GET.get('sort', ' ')
  abs = sort_accounts(abs, sort)
  
  return render(request, 'abs/index.html')

# queryset = abs = AccountBook.objects.all()
def choice_category(queryset, choice):
  # index.html에서 조회할 카테고리를 선택했으면 그에 맞는 filter를 적용한 qeurtyset을 return
  if choice == '식비':
    return queryset.filter(category='식비')
  elif choice == '카페':
    return queryset.filter(category='카페')
  elif choice == '교통비':
    return queryset.filter(category='교통비')
  elif choice == '문화생활':
    return queryset.filter(category='문화생활')
  elif choice == '의류':
    return queryset.filter(category='의류')
  # 선택한 카테고리가 없으면 filter를 적용하지 않은 기존의 queryset을 return
  else:
    return queryset


def sort_accounts(queryset, sort):
  # index.html에서 정렬 기준을 설정했으면 그에 맞는 queryset을 return
  if sort == 'amount':
    return queryset.order_by('amount')
  elif sort == 'amount_desc':
    return queryset.order_by('-amount')
  elif sort == 'date':
    return queryset.order_by('date')
  elif sort == 'date_desc':
    return queryset.order_by('-date')
  elif sort == 'pk':
    return queryset.order_by('pk')
  elif sort == 'pk_desc':
    return queryset.order_by('-pk')
  # 없으면 정렬을 적용하지 않은 queryset을 return
  else:
    return queryset
```