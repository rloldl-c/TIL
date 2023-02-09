# SQL
- 데이터베이스에 정보를 저장하고 처리하기 위한 프로그래밍 언어

## SQL Statements
- SQL 언어를 구성하는 가장 기본적인 코드 블록
```sql
SELECT column_name FROM table_name;
```
- 위 statements는 SELECT, FROM 두개의 키워드로 구성
- FROM ➡ SELECT ➡ ORDER 순서로 실행
- 수행 목적에 따라 4가지로 나눌 수 있음

    |유형|역할|SQL 키워드|
    |:---:|:---:|:----------:|
    |DDL<br>(Data Definition Language)|데이터의 기본 구조 및 형식 변경|CREATE <br> DROP<br> ALTER
    |DQL<br>(Data Query Language)|데이터 검색|SELECT|
    |DML<br>(Data Manipulation Language)|데이터 조작<br>(추가, 수정, 삭제)|INSERT<br>UPDATE<br>DELETE|
    |DCL<br>(Data Control Language)|데이터 및 작업에 대한<br>사용자 권한 제어|COMMIT<br>ROLLBACK<br>GRANT<br>REVOKE|

### Query
- SQL로 작성하는 코드
- 문장 끝에 세미콜론(;) 필수
- 키워드는 대소문자를 구분하지 않지만 대문자로 작성하는 것이 좋음
- 세미콜론만 잘 붙이면 한 문장으로 쓰든 나뉘어서 쓰든 차이는 없음

```sql
SELECT lastName FROM employees;

SELECT
    lastName
FROM
    employees;
```
<br>

## Querying
## `SELECT statement`
- SELECT 키워드 다음에 데이터를 선택하려는 필드를 하나 이상 지정
- FROM 키워드 다음에 데이터를 선택하려는 데이블의 이름을 지정
```sql
SELECT
    select_list
FROM
    table_name;
```
### 예시 데이터베이스 - purchase
|ID|name|price|quantity|discount_id|
|---|---|---|---|---|
|1|pen|7|5|1|
|2|notebook|11|8|2|
|3|rubber|11|3|1|
|4|pencil case|24|2|3|
<br>

- SELECT문에서 여러 필드 조회 가능
    ```sql
    SELECT name, price FROM purchase;
    ```

- 모든 필드를 조회하려면 `*` 입력
    ```sql
    SELECT * FROM purchase;
    ```

- `NULL`: 데이터베이스에 값이 없음을 표현하는 값
    - 파이썬에서 None타입과 동일

- `AS`로 필드명 변경 가능
    - 테이블의 필드명을 직접 바꾸는 게 아닌 출력만 해주는 것
    ```sql
    SELECT name AS '이름' FROM purchase;
    -- 원래 필드명 'name'이 아닌 '이름'으로 출력
    ```

- 기본 사칙연산 가능
    ```sql
    SELECT
        price * quantity
    FROM 
        purchase;
    ```

<br>

## Sorting
## `ORDERED BY clause`
- FROM clause 뒤에 위치
- 하나 이상의 칼럼을 기준으로 오름차순, 내림차순으로 정렬하여 출력
```sql
SELECT
    select_list
FROM
    table_name
ORDER BY
    column1 ASC
    column2 DESC;
```
- 기준이 두개 이상이면 동일한 값 하나에서 또 정렬 기준을 적용
```sql
SELECT
    price,
    quantity
FROM
    purchase
ORDER BY
    price,
    quantity DESC;
-- price가 동일한 notebook과 rubber의 quantity에 대해서만 내림차순 정렬 적용
```