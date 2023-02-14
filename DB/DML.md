# DML(Data Manipulation Language)

## 1. INSERT
```sql
INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);
```
- INSERT INTO 절 다음 테이블 이름과 필드 목록 작성
- VALUES 키워드 다음 괄호 안 필드에 삽입할 값 목록을 작성
    - 괄호 안 필드와 순서를 일치시켜야 함
```sql
INSERT INTO
	articles(title, content, createdAt)
VALUE
	('title1', 'content1', '1900-01-01'),
    ('title2', 'content2', '1800-01-01'),
    ('title3', 'content3', '1700-01-01');
```

## 2. UPDATE
```sql
UPDATE table_name
SET column_name = expression,
[WHERE
    condition];
```
- SET 다음에 수정할 필드와 새 값을 지정
- WHERE절에 수정할 레코드를 지정
    - WHERE절을 작성하지 않으면 모든 레코드가 수정됨
```sql
UPDATE
	articles
SET
	content = REPLACE(content, 'content', 'TEST');
```
- articles 테이블의 모든 content 필드의 레코드 값에 있는 'content'를 'TEST'로 변경
```sql
UPDATE 
	users
SET 
	country = 'Korea'
WHERE
	country IS NULL;
```
- users 테이블의 country 필드가 NULL인 모든 country 필드 값을 'Korea'로 변경

## 3. DELETE
```sql
DELETE FROM table_name
[WHERE
    condition];
```
```sql
DELETE FROM 
    articles
ORDER BY
    createdAt DESC
LIMIT 2;
```
- articles 테이블에서 가장 최근에 작성된 레코드 2개 삭제
