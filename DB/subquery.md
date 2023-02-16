# Subquery
- 단일 쿼리문에 여러 테이블의 데이터를 결합하는 방법
- 조건에 따라 하나 이상의 테이블에서 데이터를 검색하는 데 사용
- SELECT, FROM, WHERE, HAVING 절 등에서 다양하게 사용
- FROM 절에서 사용하는 subquery는 별도의 테이블로 간주되기 때문에 별칭(AS) 지정 필수
    - 그렇지 않으면 에러 발생(Error Code: 1248. Every derived table must have its own alias)

<br>

#### 예시 1) 테이블 customers 에서 2003년 1월 6일과 2003년 3월 26일 사이에 주문(order)을 한 고객의 customerNumber, customerName 를 조회.
```SQL
SELECT customerNumber, customerName
FROM customers
WHERE customerNumber IN (
	SELECT customerNumber
	FROM orders
	WHERE orderDate BETWEEN '2003-01-06' AND '2003-03-26'
);
```

#### 예시 2) 가장 많은 주문(order)을 한 고객(customer)의 customerNumber , customerName , 주문 수(order_count) 를 조회
```SQL
SELECT customerNumber, customerName, order_count
FROM customers
INNER JOIN  (
	SELECT customerNumber, COUNT(customerNumber) AS order_count
	FROM orders
    GROUP BY customerNumber
) AS sub USING (customerNumber)
ORDER BY order_count DESC
LIMIT 1;
```

<br>

## EXISTS   
```SQL
SELECT
    select_list
FROM
    table_name
WHERE
    [NOT] EXISTS (subquery);
```
- subquery에 하나 이상의 행이 존재하면 true 반환, 그렇지 않으면 false 반환
- 주로 subquery의 존재 여부를 확인하는 데 사용

#### 예시 1) 적어도 한 번 이상 주문한 고객의 번호와 이름 조회
```sql
SELECT customerNumber, customerName
FROM customers
WHERE
    EXISTS (
        SELECT *
        FROM orders
        WHERE customers.customerNumber = orders.customerNumber
    )
```

<br>

## CASE
```sql
CASE case_value
    WHEN when_value1 THEN statements
    WHEN when_value2 THEN statements
    ...
    [ELSE else-statements]
END CASE;
```
- case_value가 when_value와 동일한 것을 찾을 때까지 순차적으로 비교
    - 파이썬에서 if-elif와 비슷..?
- when_value와 동일한 case_value를 찾으면 해당 THEN절의 코드 실행
- 동일한 값을 찾지 못하면 ELSE절의 코드 실행
    - ELSE절이 없는 경우엔 오류
    
#### 예시) orders 테이블의 status에 따라 상새 정보를 매겨 조회
```sql
SELECT orderNumber, status,
    CASE
        WHEN status = 'In Process' THEN '주문중'
        WHEN status = 'Shipped' THEN '발주완료'
        WHEN status = 'Cancelled' THEN '주문취소'
        ELSE '기타사유'
    END AS details
FROM orders;
```