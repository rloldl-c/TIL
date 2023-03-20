# Framework
- 웹 어플리케이션을 빠르게 개발할 수 있도록 도와주는 도구
    - 개발에 필요한 기본 구조, 규칙, 라이브러리 등을 제공)
- 장점
    - 기본적인 구조와 규칙을 제공하기 때문에 필수적인 개발에만 집중 가능
    - 여러 라이브러리를 제공해 개발 속도를 빠르게 할 수 있음
    - 유지보수와 확장에 용이

# 클라이언트와 서버
- client: 서비스를 요청하는 주체
    - 웹 사용자의 인터넷이 연결된 장치, 브라우저)
- server: 요청에 응답하는 주체
    - 웹 페이지, 앱을 저장하는 컴퓨터
- 웹 페이지를 보는 과정
    1. 사용자가 웹 브라우저(**클라이언트**)에서 'google.com'을 입력
    2. 브라우저는 인터넷에 연결된 구글 컴퓨터(**서버**)에게 html 파일을 달라고 요청
    3. 요청을 받은 컴퓨터는 데이터베이스에서 html 파일을 찾아 브라우저 컴퓨터에게 전달
    4. 웹 브라우저가 도착한 html 파일을 읽어서 화면에 출력


# Django
## Setting up a development environment
### 0. `.gitignore` 만들기
- [gitignore.io](https://www.toptal.com/developers/gitignore/)에서 `Windows`, `macOS`, `VisualStudioCode`, `Python`, `Django` 검색 후 생성된 내용 복사
### 1. 가상환경 생성
`python -m venv venv`
- 가상환경 이름은 `venv` 권장
### 2. 가상환경 활성화
- in Git Bash<br>
`source venv/Scripts/activate`
- in VS Code<br>
    1. 터미널 창이 열려 있다면 닫기
    2. ctrl + shift + p
    3. interpreter 입력 후 `Python: Select Interpreter`
    4. 가상환경(venv)에 있는 python 선택
### 3. Django 설치
`pip install django==3.2.18`
### 4. 의존성 파일 생성
`pip freeze > requirements.txt`
- 파일 이름은 `requirements` 권장
- 패키지 설치시 항상 진행
### 4-1. 의존성 파일로 패키지 설치하기
`pip install -r requirements.txt`
### 5. Django 프로젝트 생성
`django-admin startproject (project_name) .`
### 6. Django 서버 실행
`python manage.py runserver`
