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

## 1. Querying
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

## 2. Sorting
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

<br>

## 3. Filtering
### 1) 중복 제거
```sql
SELECT DISTINCT
    select_list
FROM
    table_name;
```
- SELECT 키워드 바로 뒤에 작성
- SELECT DISTINCT 다음에 고유한 값을 선택하려는 하나 이상의 필드를 지정

<br>

### 2) 검색 조건 지정
```sql
SELECT
    select_list
FROM
    table_name
WHERE
    search_condition;
```
- FROM clause 뒤에 위치
- 비교 연산자 및 논리 연산자를 사용하여 조건을 지정
1. `BETWEEN`
    - 테이블 employees에서 officeCode 필드 값이 1에서 4 사이 값인 데이터의 lastName, firstName, officeCode를 오름차순 조회
    ```sql
    SELECT
        lastName, firstName, officeCode
    FROM
        employees
    WHERE
        officeCode BETWEEN 1 AND 4
    ORDER BY
        officeCode;
    ```

2. `IN`
    - 테이블 employees에서 officeCode 필드 값이 1 또는 3 또는 4인 데이터의 lastName, firstName, officeCode를 조회
    ```sql
    SELECT
        lastName, firstName, officeCode
    FROM
        employees
    WHERE
        officeCode IN (1, 3, 4)
    ```

3. Wildcard
    - `LIKE`와 함께 사용
    - `%` : 0개 이상의 문자열과 일치하는지 확인
    - `_` : 단일 문자와 일치하는지 확인

        |operator|description|
        |--------|-----------|
        |`LIKE 'a%'`| 'a'로 시작하는 데이터|
        |`LIKE '%a'`| 'a'로 끝나는 데이터|
        |`LIKE '%or%'`|'or'을 포함하는 데이터|
        |`LIKE '_r%'`| 'r'이 두번째로 오는 데이터|
        |`LIKE 'a_%_%'`|'a'로 시작하면서 길이가 최소 3인 데이터'|

### 3) 조회하는 레코드 수 제한
```sql
SELECT
    select_list
FROM
    table_name
LIMIT [offset,] row_count;
```
- LIMIT clause는 하나 또는 두 개의 인자를 사용
- row_count는 조회할 최대 레코드 수를 지정
- ex) 테이블 customers에서 contactFirstName, creditLimit 필드 데이터를 creditLimit 기준 4번째로 높은 데이터부터 7번째 데이터까지 조회
```sql
SELECT
    contactFirstName, creditLimit
FROM
    customers
ORDER BY
    creditLimit DESC
LIMIT 3, 4;
-- LIMIT 4 OFFSET 3;
```

<br>

## 4. Grouping
- 레코드를 그룹화하여 요약본 생성(with 집계함수)
```sql
SELECT
    c1, c2, ..., cn, aggregate_function(ci)
FROM
    table_name
GROUP BY
    c1, c2, ..., cn;
```
- FROM 및 WHERE 절 뒤에 배치
- GROUP BY 절 뒤에 그룹화할 필드 목록 작성
- aggregate function
    
    |name|description|
    |----|----------|
    |`AVG()`|그룹의 평균 계산|
    |`COUNT()`|그룹의 개수 계산|
    |`MAX()`|그룹에서 최대값 계산|
    |`MIN()`|그룹에서 최소값 계산|
    |`SUM()`|그룹의 총합 계산|

### `HAVING clause`
- 그룹에는 WHERE 대신 HAVING으로 세부 조건을 지정
- ex) 테이블 customers에서 country 필드를 그룹화하여 각 그룹에 대한 creditLimit의 평균 값이 80000을 초과하는 데이터 조회
    ```sql
    SELECT
        country, AVG(creditLimit)
    FROM
        customers
    GROUP BY
        country
    HAVING
        AVG(creditLimit) > 80000;
    ```

## 참고
### SELECT statement 작성 순서
1. SELECT
2. FROM
3. WHERE
4. GROUP BY
5. HAVING
6. ORDER BY
7. LIMIT

### SELECT statement 실행 순서
1. FROM: 테이블에서
2. WHERE: 특정 조건에 맞춰
3. GROUP BY: 그룹화 하고
4. HAVING: 그룹 중에 조건이 있다면 맞춰서
5. SELECT: 조회하여
6. ORDER BY: 정렬한 후
7. LIMIT: 특정 위치의 값을 가져온다