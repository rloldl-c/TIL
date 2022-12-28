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


