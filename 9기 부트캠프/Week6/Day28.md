# Day28 요약

## join

* 여러 개의 테이블을 연결하여 하나의 테이블을 만드는 과정.
* join 할 때는 작은 것부터 조인하는 것이 성능에 좋음.
* INNER JOIN
    * 등가 조인(EQUIJOIN)
    * 비등가 조인 (NON-EQUIJOIN)
        * 등급매길 때 사용
* OUTER JOIN
    * LEFT OUTER JOIN
    * RIGHT OUTER JOIN
* SELF JOIN
    * 자신의 상사를 조회하는 경우 
* CROSS JOIN
* FULL OUTER JOIN

## Dictionary 

* ORACLE SERVER에 의해서 생성되고 유지보수되는 것
* 데이터베이스에 대한 정보만 가지고 있음.
    * 오라클 사용자 정보, 권한과 롤 정보
    * 스키마 객체에 대한 정보
    * 무결성 제약조건에 관한 정보
    * 데이터 베이스 구조 정보
    * 함수와 프로시저, 트리거에 대한 정보
* 읽기 전용으로 제공되는 뷰와 테이블의 집합

**Dictionary View 종류**

* USER : 사용자가 소유한 객체에 관한 정보 저장
* ALL : 사용자에게 액세스가 허용된 객체 관한 정보 저장
* DBA : DBA 권한을 가진 사용자가 액세스 할 수 있는 정보 저장
* V$ : 서버의 성능과 Locking에 관한 정보 저장

## SEQUENCE

```SQL
CREATE SEQUENCE ID 
    INCREMENT BY 1
    START WITH 26
    MAXVALUE 99999999
    NOCACHE
    NOCYCLE;

SELECT * FROM USER_SEQUENCES;   -- 시퀀스 정보
INSERT INTO S_EMP (ID, NAME, SALARY) VALUES (ID.NEXTVAL, 'TEST', 10000);    -- 사용 가능한 다음 SEQUENCE 값 반환
SELECT ID.CURRVAL FROM DUAL;    -- 현재 SEQUENCE 값 포함
```

* 자동으로 Unique Number 을 생성
* 일반적으로 PK 값 생성을 위해 사용
* START WITH N - 생성되는 첫번째 SEQUENCE 번호, 생략되면 1부터 시작함.
* MAXVALUE - 생성 가능한 SEQUENE의 최대값
* NOCACHE - 메모리에 유지할 값의 수
* NOCYCLE - 최대값이나 최소값까지 값이 생성된 경우에도 값을 생성시키는 것 기본은 NOCYCLE 

## VIEW

```SQL
create or replace view v_emp
as 
    select 
        *
    from 
        s_emp_2023_11_22
    where 
        start_date like '%15%';
```

* 15년도에 해당하는 데이터 v_emp View 생성방법
* FORCE 옵션 - 존재하지 않을경우 오류는 발생하지만 뷰는 생성
* WITH READ ONLY - select만 가능하고 dml은 사용불가.

## SYNONYM (시노님)

```SQL
create synonym e for s_emp;
```
* 스키마명을 붙이지 않고 테이블을 사용하는 일종의 별칭
* 오브젝트명을 짧게함으로써 SQL문 단순화
* PUBLIC 옵션은 DBA만 생성가능