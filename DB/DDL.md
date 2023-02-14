# DDL(Data Definition Language)

## 1. CREATE
```sql
CREATE TABLE table_name (
    column1 data_type,
    column2 data_type,
    ...,
    constraints
);
```
- 각 필드에 적용할 데이터 타입 작성
- 테이블 및 필드에 대한 제약조건 작성

<br>

```sql
CREATE TABLE posts (
	postId INT AUTO_INCREMENT,
    title VARCHAR(50) NOT NULL,
    content VARCHAR(200) NOT NULL
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (postId)
);
```
- constraint: 데이터의 무결성을 지키기 위해 데이터를 입력받을 때 실행하는 검사 규칙
    - PRIMARY KEY: 해당 필드를 기본 키로 지정
    - NOT NULL: 해당 필드에 NULL값을 저장하지 못하도록 지정
    - DEFAULT: 데이터 입력시 해당 필드 값을 따로 작성하지 않으면 설정된 기본값으로 저장

- AUTO_INCREMENT: 기본 키에 대한 번호 자동 생성
    - 시작 값은 1이며, 데이터 입력시 값을 생략하면 자동으로 1씩 증가
    - 이미 사용한 값을 재사용하지 않음(데이터를 삭제해도 그 값이 아닌 다른 값을 부여)
    - 기본적으로 NOT NULL 포함

## 2. DROP
```sql
DROP TABLE table_name;
```

## 3. ALTER
### 1) ADD
```sql
ALTER TABLE
    table_name
ADD
    new_column_name column_definition;
```
- ADD 키워드 뒤에 추가하고자 하는 필드 이름과 데이터 타입 및 제약조건 작성
```sql
ALTER TABLE
	posts
ADD writer VARCHAR(100),
ADD address VARCHAR(100) NOT NULL;
```

### 2) MODIFY
```sql
ALTER TABLE
    table_name
MODIFY
    column_name column_definition;
```
```sql
ALTER TABLE
    posts
MODIFY
    writer VARCHAR(20) DEFAULT 'Anonymous';
```

### 3) CHANGE
```sql
ALTER TABLE
    table_name
CHANGE COLUMN
    original_name new_name column_definition;
```
- 기존 필드 이름, 변경하고자 하는 필드 이름, 데이터 타입 및 제약조건을 순서대로 작성
```sql
ALTER TABLE
    posts
MODIFY
    writer name VARCHAR(20) DEFAULT 'Anonymous';
```
- 데이터 타입 및 제약조건에 변경사항이 없더라도 작성해줘야 함

### 4) DROP
```sql
ALTER TABLE
    table_name
DROP COLUMN
    column_name;
```
```sql
DROP TABLE IF EXISTS posts;
```
- posts 테이블이 존재하면 posts 테이블을 삭제