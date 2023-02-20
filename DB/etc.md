# Transaction
- 여러 쿼리를 묶어서 하나의 작업처럼 처리하는 방법
- 하나로 묶인 쿼리는 모두 실패하거나 성공하거나 둘 중 하나
```sql
START TRANSACTION;
state_ments;
...
[ROLLBACK | COMMIT];
```
- START TRANSACTION : 트랜잭션 구문의 시작
- COMMIT : 모든 작업이 정상적으로 완료되면 한꺼번에 DB에 반영
- ROLLBACK : 부분적으로 작업이 실패하면 트랜잭션에서 진행한 모든 연산을 취소하고 트랜잭션 실행 전으로 되돌림

<br>

# Trigger
- 특정 이벤트에 대한 응답으로 자동으로 실행되는 것
- DML의 영향을 받는 필드값에만 적용 가능(INSERT, UPDATE, DELETE)
```SQL
CREATE TRIGGER trigger_name
{BEFORE | AFTER} {INSERT | UPDATE | DELETE}
ON table_name FOR EACH ROW
trigger_body;
```
- CREATE TRIGGER 키워드 다음에 생성하려는 트리거 이름 지정
- 각 레코드의 어느 시점에 트리거가 실행될지 지정
- ON 키워드 뒤에 트리거가 속한 테이블의 이름을 지정
- 트리거가 활성화될 때 실행할 코드를 trigger_body에 지정
    - 여러 명령문을 실행하려면 BEGIN END 키워드로 묶어서 사용

#### ex 1) 기존 게시글이 수정되면, 게시글의 수정일자 필드값을 최신 일자로 업데이트 하기
```sql
DELIMITER //
CREATE TRIGGER beforeArticleUpdate
    BEFORE UPDATE
    ON articles FOR EACH ROW
BEGIN
    SET NEW.updateAt = CURRENT_TIME();
END //
DELIMITER ;
```
- DELIMITER : BEGIN-END 구문 사이에 여러 SQL문이 작성되기 때문에 하나의 구문으로 작동할 수 있도록 구문 문자 변경
- OLD/NEW : 트리거에서 특정 시점 전/후의 값에 접근할 수 있도록 제공하는 키워드

    |   | OLD |NEW|
    |---|---|---
    |INSERT| O | X|
    |UPDATE|O|X|
    |DELETE|X|O|

#### ex 2) 트리거를 사용해 게시글이 작성되면, 별도의 테이블에 몇 번 게시글이 작성되었따는 것을 기록하기
```sql
DELIMITER //
CREATE TRIGGER recordLogs
    AFTER INSERT
    ON articles FOR EACH ROW
BEGIN
    INSERT INTO articleLogs (description, createdAt)
    VALUES (CONCAT(NEW.id, '번 글이 작성되었습니다.'), CURRENT_TIME());
END//
DELIMITER ;
```