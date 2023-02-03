# 파일 입출력

## 파일 입력
### open(file, mode='r', encoding=None)
- file: 파일명
- mode: 텍스트 모드

  |character|meaning|
  |---------|-------|
  |'r'|open for reading(default)|
  |'w'|opne for writing, truncating the file first (덮어쓰기)|
  |'a'|opne for writing, appending to the end of file if it exists (이어쓰기)|

- encoding: 인코딩 방식(일반적으로 UTF-8 활용)

### 파일 활용
- 파일 객체 활용
  - close() 필수
  ```python
  f = opne('file_name', 'r', encoding='UTF8')
  f.close()
  ```

- with 키워드 활용
  - 블록을 벗어나서 작성하면 열린 파일이 자동으로 close 되므로 주의해서 작성
  ```python
  with opne('file_name', 'r', encoding='UTF8') as f:
      line = f.read()
  ```

### 파일 읽기
1. readline()
  - 파일의 첫 줄을 읽는 함수
  - 줄이 개행(`\n`)으로 끝난다면 같이 읽음
    - `.strip()` 함수를 사용하면 `\n` 제거 가능
  - 파일의 모든 줄을 읽고 싶다면 반복문을 활용
  ```python
  with opne('file_name', 'r', encoding='UTF8') as f:
      while True:
        line = f.readline()
        if not line: # line이 없으면
          break
        print(line)
  ```

2. readlines()
  - 파일의 모든 줄을 읽어 리스트로 반환

3. read()
  - 파일의 전체 내용을 문자열로 반환

## JSON
- 자바 스크립트 객체 표기법으로 웹 어플리케이션에서 데이터를 전송할 때 일반적으로 사용하는 데이터 양식

### JSON 파일의 활용
- `improt json`을 선언해야 json 파일 활용 가능
- `json.load()`로 json 파일을 읽음
    - 딕셔너리 자료형으로 반환