# 오늘 한 일
## axios
### `FormData`
- 로그인 등 폼 데이터를 axios로 전송해야할 때
```javascript
// javascript - axios

const username = ...
const password = ...
const csrftoken = ...

loginForm.addEventListener('submit', function (event) {
  event.preventDefault();
  const form = new FormData()
  form.append('username', username)
  form.append('password', password)
  form.append('csrfmiddlewaretoken', csrftoken)

  axios({
    method: 'post',
    url: '...',
    headers: {'X-CSRFToken': csrftoken},
    data: form,
  })
  .then((response) => {
    if (response.data.valid) {
      // 로그인에 성공하면 페이지 새로고침
      location.reload()
    } else {
      // 로그인에 실패했을 경우 실행할 코드
    }
  })
})
```
```python
# views

def login(request):
    if request.method == 'POST':
        form = AuthenticationForm(request, request.POST)
        if form.is_valid:
            auth_login(request, form.get_user())
            return JsonResponse({'valid': True})
        else:
        form = CustomAuthenticationForm()

    context = {
        'valid': False,
    }
    return JsonResponse(context)
```
<br>

#### `FormData.append()`
- FormData 객체 안에 키가 이미 존재하면 그 키에 새로운 값으로 갱신하고, 없으면 추가
<br>

#### 이미지 업로드 하기
- 헤더에 `'Content-Type": "multipart/form-data'` 추가
```javascript
axios({
  headers: {
    'Content-Type": "multipart/form-data',
  }
  url: // 이미지 업로드 요청 url
  method: 'post',
  data: formData,
})
```