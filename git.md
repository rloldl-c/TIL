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

**$ git add \<file>**
- working directory에서 변경 내용을 staging area에 추가하기 위해 사용
- untracked변화없음) 상태(의 파일을 staged로 변경
- modified(변화는 있으나 add 실행 전) 상태의 파일을 staged로 변경

**$ git commit -m '<커밋메시지>'**
- staged 상태의 파일들을 커밋을 통해 버전으로 기록
- 커밋 메시지는 변경 사항을 나타낼 수 있도록 명확하게 작성

\* 파일을 수정하였을 때 버전으로 기록하고 싶다면 add, commit

**$ git log**
- 현재 저장소에 기록된 커밋을 조회
- add와 commit 모두 완료한 버전만 조회 가능
- 다양한 옵션으로 조회 가능
  - -1, --oneline 등

**$ git status**
- git 저장소에 있는 파일의 상태를 확인
- working directory와 staging area의 파일들만 확인 가능

### 여러 메시지들
1. untracked files: 어떠한 파일을 만들었지만 add 하지 않은 상태
2. changes to be committed: 파일을 만들고 add까지 완료한 상태
3. nothing to commit, working tree clean: 수정사항 없이 add와 commit 모두 완료한 상태
4. changes not staged for commit: 커밋된 적 있는 파일을 수정한 상태

\* unmodified: 변화 없음<br>
\* modified: 변화가 있으나 stagig area로 옮기지 않은 상태(add를 하지 않은 상태)<br>
\* staged: add 명령어로 staging area로 옮김