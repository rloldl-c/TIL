# Cookie & Session
## HTTP
- HTML 문서와 같은 리소스들을 가져올 수 있도록 해주는 규약
- 웹에서 이루어지는 모든 데이터 교환의 기초
### 특징
- connectionless: 서버는 요청에 대한 응답을 보낸 후 연결을 끊음
- stateless: 연결을 끊는 순간 클라이언트와 서버 간의 통신이 끝나며 상태 정보가 저장되지 않음
  - 로그인이 유지되지 않거나 장바구니 목록이 사라짐
<br>

## Cookie
### 사용 예시
1. 브라우저는 서버에게 영어가 아닌 한글로 보여달라고 요청
2. 서버는 해당 정보가 저장된 쿠키를 브라우저에게 응답
3. 해당 페이지를 다음에 다시 방문했을 때 브라우저가 서버에게 쿠키를 요청하고, 서버는 그에 해당하는 웹페이지를 응답

### 사용 목적
- 세션 관리: 로그인, 아이디 자동완성, 공지 하루 안 보기, 장바구니 등의 정보 관리
- 개인화(Personalization): 사용자 선호, 테마 등 관리
- 트래킹(Tracking): 사용자 행동 기록 및 분석

## Session
- 서버 측에 생성되어 클라이언트와 서버 간의 상태를 유지
- 상태 정보를 저장하는 방식
### 작동 예시
1. 클라이언트가 로그인을 하면 서버가 세션 데이터를 생성 후 저장
2. 생성된 세션 데이터에 인증할 수 있는 세션 ID 발급
3. 발급한 세션 ID를 클라이언트에게 응답
4. 클라이언트는 받은 세션 ID를 쿠키에 저장
5. 클라이언트가 다른 페이지로 이동하면 요청과 함께 세션 ID가 저장된 쿠키를 서버에 전달
6. 서버는 세션 ID를 확인해서 로그인 상태를 유지
