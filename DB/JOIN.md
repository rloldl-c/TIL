# JOIN
- 둘 이상의 테이블에서 데이터를 검색하는 방법
## INNER JOIN
```sql
SELECT
    select_list
FROM
    table1
INNER JOIN table2
    ON table1.fk = table2.pk;
```
- 두 테이블에서 값이 일치하는 레코드만 조회
- FROM 절 이후 메인 테이블 지정
- INNER JOIN 절 이후 메인 테이블과 조인할 테이블을 지정
- ON 키워드 이후 조인 조건(table1과 table2의 레코드를 일치시키는 규칙)을 작성

<br>

```sql
CREATE TABLE users (
	id INT AUTO_INCREMENT,
    name VARCHAR(50) NOT NULL,
    PRIMARY KEY (id)
);

DROP TABLE users;

CREATE TABLE articles(
	id INT AUTO_INCREMENT,
    title VARCHAR(50) NOT NULL,
    cotent VARCHAR(100) NOT NULL,
    userId INT NOT NULL,
    PRIMARY KEY (id)
);

INSERT INTO
	users (name)
VALUE
	("권미자"),
    ("류준하"),
    ("정영식");
    
INSERT INTO
	articles (title, cotent, userId)
VALUES
	("제목1", "내용1", 1),
    ("제목2", "내용2", 2),
    ("제목3", "내용3", 4);

SELECT *
FROM articles
INNER JOIN users
    ON articles.userId = users.id;
```
- INNER JOIN 결과

    |id|title|content|userId|id|name|
    |--|----|----|----|---|---|
    |1|제목1|내용1|1|1|권미자|
    |2|제목2|내용2|2|2|류준하|

<br>

## LEFT JOIN
```sql
SELECT
    select_list
FROM
    table1
LEFT JOIN table2
    ON table1.fk = table2.pk;
```
- 왼쪽 테이블의 모든 레코드와 조건에 일치하는 오른쪽 레코드 조회
    - 왼쪽 테이블에서 NULL값을 가진 레코드 존재
- FROM절 이후 왼쪽 테이블 지정
- LEFT JOIN절 이후 오른쪽 테이블 지정
- 왼쪽은 무조건 표시하고, 매치되는 레코드가 없으면 NULL을 표시
- 왼쪽 테이블 한 개의 레코드에 여러 개의 오른쪽 테이블 레코드가 일치할 경우, 해당 왼쪽 레코드를 여러 번 표시
```sql
SELECT *
FROM articles
LEFT JOIN users
    ON articles.userId = user.id;
```
- LEFT JOIN 결과

    |id|title|content|userId|id|name|
    |--|----|----|----|---|---|
    |1|제목1|내용1|1|1|권미자|
    |2|제목2|내용2|2|2|류준하|
    |3|제목3|내용3|4|NULL|NULL|

    - articles 테이블에선 userId가 4인 레코드가 존재하지만, users 테이블에서는 id가 4인 레코드가 없으므로 NULL값으로 출력

<br>

## RIGHT JOIN
```sql
SELECT
    select_list
FROM
    table1
RIGHT JOIN table2
    ON table1.fk = table2.pk;
```
- 오른쪽 테이블의 모든 레코드와 조건에 일치하는 왼쪽 레코드 조회
    - 오른쪽 테이블에서 NULL값을 가진 레코드 존재
- FROM절 이후 왼쪽 테이블 지정
- RIGHT JOIN절 이후 오른쪽 테이블 지정
- 오른쪽은 무조건 표시하고, 매치되는 레코드가 없으면 NULL을 표시
- 오른쪽 테이블 한 개의 레코드에 여러 개의 왼쪽 테이블 레코드가 일치할 경우, 해당 오른쪽 레코드를 여러 번 표시

```sql
SELECT *
FROM articles
RIGHT JOIN users
    ON articles.userId = user.id;
```
- LEFT JOIN 결과

    |id|title|content|userId|id|name|
    |--|----|----|----|---|---|
    |1|제목1|내용1|1|1|권미자|
    |2|제목2|내용2|2|2|류준하|
    |NULL|NULL|NULL|NULL|3|정영식|

    - users 테이블에선 id가 3인 레코드가 존재하지만, articles 테이블에서는 userId가 3인 레코드가 없으므로 NULL을 출력

<br>

## FULL OUTER JOIN
```SQL
SELECT *
FROM table1
LEFT JOIN table2
    ON table1.fk = table2.pk;
UNION
SELECT
FROM
RIGHT JOIN
    ON table1.fk = table2.pk;
```
- 모든 레코드 조회
- table1에는 존재하고 table2에는 존재하지 않는 레코드, table2에는 존재하고 table1에는 존재하지 않는 레코드는 NULL로 표시

<br>

### * 기본키와 외래키 필드 명이 같은 경우
```sql
SELECT *
FROM table1
INNER JOIN table2 USING (column)
```