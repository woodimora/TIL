# DDL (Data Definition Language) - 데이터 정의어
데이터 베이스를 정의하는 언어이며 데이터를 생성, 수정, 삭제하는 등의 데이터의 전체의 골격을 결정하는 언어. SCHEMA, DOMAIN, TABLE, VIEW, INDEX 를 정의하거나 변경 또는 삭제할 때 사용한다.

CREATE : 데이터베이스, 테이블 등을 생성하는 역할   
ALTER : 테이블을 수정하는 역할   
DROP : 데이터베이스, 테이블을 삭제하는 역할   
TRUNCATE : 테이블을 초기화 시키는 역할


# DML (Data Manipulation Language) - 데이터 조작어
정의된 데이터 베이스에 입력된 레코드를 조회하거나 수정하거나 삭제하는 역할.데이터베이스의 사용자가 응용 프로그램이나 질의어를 통하여 저장된 데이터를 실질적으로 처리하는데 사용하는 언어

SELECT : 데이터를 조회   
INSERT : 데이터를 삽입   
UPDATE : 데이터를 수정   
DELETE : 데이터를 삭제   


# DCL (Data Contol Language) - 데이터 제어어
데이터베이스에 접근하거나 객체에 권한을 주는 역할. 데이터의 보안, 무결성, 회복 등을 정의하는데 사용

GRANT : 특정 데이터베이스 사용자에게 특정 작업에 대한 수행권한을 부여   
REVOKE : 특정 데이터베이스 사용자에게 특정 작업에 대한 수행 권한을 박탈, 회수   
COMMIT : 트랜젝션의 작업이 정상적으로 완료되었음을 알리는 역할   
ROLLBACK : 트랜젝션의 작업이 비정상적으로 종료되었을 떄 원래 상태로 복구하는 역할