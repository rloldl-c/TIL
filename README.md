# 마크다운 문법 정리

## Heading
- 문서의 제목이나 소제목
- #의 개수에 따라 heading level이 정해짐(h1~h6까지)

## List
- 순서가 있는 리스트(ol)와 순서가 없는 리스트(ul)로 구성
- tab으로 하위 항목 구성 가능
- ol: 1. text
- ul: - text / * text

## Fenced Code block
- backtick(`) 기호 3개를 사용하여 작성
```python
printf("hello")
```

## Inline Code block
- backtick 기호 1개를 사용하여 작성

## Link
- []에 문자열을 넣고 ()에 url을 넣어 사용
- [naver](https://naver.com)
- 파일이나 폴더도 삽입 가능

## Image
- 링크 문법 앞에 !를 붙여서 사용
- ![text](image.jpg)
- 다른 폴더에 있는 이미지를 불러오기 위해서는 파일 경로 필요

## Blockquote
- '>' 뒤에 text 입력
>이런 식으로 보여짐

## 텍스트 효과
- bold: ** / __ 사이에 텍스트를 넣어서 사용
- **bold text**
- italic: * / _ 사이에 텍스트를 넣어서 사용
- *italic*

# CLI(Commnad Lin Interface)
## CIL?
- CLI(**명령어** 인터페이스): 터미널을 통해 사용자와 컴퓨터가 상호작용 하는 방식
- 입력: 사용자가 키보드 등을 통한 문자열
- 출력: 문자열
- 셸: 위와 같은 인터페이스를 제공하는 프로그램(ex. command.com)

## CLI 구성요소
- 컴퓨터 정보
- 디렉토리('~'의 경우 홈 디렉토리를 의미)
- $: 명령어 입력

### 기초 파일 시스템 명령어
- ls : 파일 목록 확인
- mkdir 문자열 : 새로운 폴더 생성
- touch 문자열(확장자 포함) : 빈 파일 생성
- cd 문자열 : 하위 폴더로 이동
- cd .. : 한 단계 상위 폴더로 이동
- rm 문자열 : 파일 삭제
- rm -r 문자열 : 폴더 삭제

# Git
- Git: 분산버전관리시스템으로 코드의 버전을 관리하는 도구
- 파일의 변경 사항을 추적하고 여러 사용자들 간에 파일 작업을 조율

### 중앙집중식버전관리시스템 vs 분산버전관리시스템
- 중앙집중식
  - 로컬에서는 파일을 편집하고 서버에 반영
  - 중앙 서버에서만 파일을 관리
- 분산버전
  - 로컬에서도 버전을 기록하고 관리
  - 원격 저장소를 활용하여 협업

### 저장소 생성
- $ git init
- 특정 폴더에 git 저장소(.git)를 만들고 버전 관리
  - 이 저장소는 숨김 폴더라 ls로 보이지 않음
- (master)가 없으면 git으로 관리되기 전 단계

### 버전 관리 흐름
- 작업 > 수정한 파일 모아서 add > 버전으로 기록 commit

### $ git add \<file>
- working directory에서 변경 내용을 staging area에 추가하기 위해 사용
- untracked변화없음) 상태(의 파일을 staged로 변경
- modified(변화는 있으나 add 실행 전) 상태의 파일을 staged로 변경

### $ git commit -m '<커밋메시지>'
- staged 상태의 파일들을 커밋을 통해 버전으로 기록
- 커밋 메시지는 변경 사항을 나타낼 수 있도록 명확하게 작성

\* 파일을 수정하였을 때 버전으로 기록하고 싶다면 add, commit

### $ git log
- 현재 저장소에 기록된 커밋을 조회
- add와 commit 모두 완료한 버전만 조회 가능
- 다양한 옵션으로 조회 가능
  - -1, --oneline 등

### $ git status
- git 저장소에 있는 파일의 상태를 확인
- working directory와 staging area의 파일들만 확인 가능

## 여러 메시지들
1. **untracked files**: 어떠한 파일을 만들었지만 add 하지 않은 상태
2. **changes to be committed**: 파일을 만들고 add까지 완료한 상태
3. **nothing to commit, working tree clean**: 수정사항 없이 add와 commit 모두 완료한 상태
4. **changes not staged for commit**: 커밋된 적 있는 파일을 수정한 상태

\* unmodified: 변화 없음<br>
\* modified: 변화가 있으나 stagig area로 옮기지 않은 상태(add를 하지 않은 상태)<br>
\* staged: add 명령어로 staging area로 옮김

# 원격저장소
## 원격저장소 관리
- 저장소 연결하기
  - $ git remote add origin \<url>
- 저장소에 버전 업로드
  - $ git push \<원격저장소이름> \<브랜치이름>
- 저장소에 버전 가져오기
  - $ git p \<원격저장소이름> \<브랜치이름>
- 다른 원격저장소에 있는 버전 가져오기
  - $ git clone \<url>
- 원격 저장소는 항상 최신 버전만을 보여줌

### 오류 메시지
Updates were rejected because the remote contains work that you do not have locally. ~
- 원격저장소 버전이랑 로컬 버전이랑 다르니까 git pull 명령어를 사용해서 최신 버전을 받아와
* 해결방법
1. 원격저장소에 있는 commit을 로컬로 가져오기(pull)
2. 로컬에서 두 commit을 병합 -> 동시에 같은 파일이 수정된 경우 merge conflict 발생(3일차에 배울 내용)
3. 다시 원격저장소로 push

## gitignore
: git으로 관리하지 않을 파일/폴더를 지정해주는 것
- .gitignore 파일을 하나 만들고 그 안에 git으로 관리하지 않을 파일/폴더명을 작성
  - 확장자로도 관리 가능 > *.pptx: pptx를 모두 무시해라
- 이미 commit한 파일/폴더도 무시할 수 있을까?
  - 안된다... 처음부터 잘 설정하자
- [gitignore.io](​https://gitignore.io/) 에서 원하는 설정을 검색해서 편하게 복붙 가능