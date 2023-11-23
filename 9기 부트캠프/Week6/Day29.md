# Day29 요약

## Constraint

* 무결성(Integrity)과 일관성(Consistency)
* 무결성은 결함이 없어야함 (잘못된 data x)

## INDEX

* B*TREE 검색방법으로 디스크 입출력 횟수를 줄임.
* 테이블과는 독립적임.
* 자동으로 생성되기도 하고 필요에 의해 만들기도함.
* ORACLE Server 가 자동적으로 사용하고 유지보수함.

**만드는 때**

1. 조건절이나 조인 조건의 컬럼을 자주 이용할 때
2. 컬럼이 넓은 범위 값을 가질 때
3. 많은 NULL 값을 갖을 때

**만들지 않아야될 때**

1. 테이블이 자주 변경될 때
2. 테이블이 작을 때
3. 조회 조건으로 사용되는 경우가 별로 없을 때

## VIEW

* 테이블이나 다른 뷰를 기초로 한 가상의 테이블
* 보안상의 이유로 데이터베이스에 대한 액세스를 제한함.

## CORRELATED SubQUERY

* 상호연관 쿼리
* Subquery에서 외부테이블의 값을 참조할 때 사용
* 일반 서브쿼리와는 다르게 읽어온 행을 갖고 Inner쿼리를 실행하는 것을 반복하는 것.
* ex) 소속된 부서의 평균 급여보다 많은 급여를 받는 사원을 출력하시오.
```SQL
SELECT
    FIRST_NAME
    ,JOB_ID
    ,DEPARTMENT_ID
    ,SALARY
FROM EMPLOYEES E
WHERE SALARY > (
    SELECT 
        ROUND(AVG(SALARY))
    FROM EMPLOYEES
    WHERE DEPARTMENT_ID = E.DEPARTMENT_ID
)
AND DEPARTMENT_ID < 60;
```