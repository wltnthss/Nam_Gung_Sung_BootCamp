# 여섯째 주

## SQL - ORACLE 요약

**DDL,DML, DCL, TRANSACTION**

1. DDL  
    * CREATE, ALTER, DROP, RENAME, TRUNCATE, COMMENT
2. DML
    * SELECT, INSERT, UPDATE, DELETE
3. DCL
    * GRANT, REVOKE
4. TRANSACTION
    * COMMIT, ROLLBACK, SAVEPOINT

**DISTINCT**

* SELECT 절에 DISTINCT 키워드를 통해서 중복을 제거 가능함.
* 컬럼이 여러 개면 여러 개의 컬럼에 대해서 중복을 제거함.
* FOR문을 돌면서 중복을 제거하기 때문에 성능이 좋지 않음.
* GROUP BY 도 중복을 제거해주지만 GROUP BY 는 집게함수를 쓸 때 사용하고 그게 아니면은 가독성이 좋은 DISTINCT 를 사용하자.

**DISTINCT COUNT연산 파히기**

```SQL
SELECT p_date
	, COUNT(DISTINCT column_name)
FROM table_name
WHERE p_date BETWEEN DATE_FORMAT('20211006', 'yyyy-MM-dd') AND DATE_FORMAT('20211008', 'yyyy-MM-dd')
GROUP BY p_date

-- 튜닝 후 
SELECT p_date
	, COUNT(column_name)
FROM (
	SELECT p_date
	    , column_name
	FROM table_name
	WHERE p_date BETWEEN DATE_FORMAT('20211006', 'yyyy-MM-dd') AND DATE_FORMAT('20211008', 'yyyy-MM-dd')
	GROUP BY p_date, column_name
) tmp
GROUP BY p_date
```

* 튜닝 후에 수정된 쿼리는 서브 쿼리 안에서 GROUP BY 를 통해 중복이 제거된 중간 데이터 결과 셋을 생성함.
* GROUP BY 연산은 다수의 리듀스가 작업을 분배하여 처리하여 결과적으로 제일 바깥에 있는 COUNT 연산은 크기가 감소된 중간 데이터 결과 셋을 입력으로 사용함.

**ORACLE JOIN**

1. INNER JOIN 

    * EQUIJOIN - 컬럼이 있는 값들이 = 연산자를 사용하여 정확하게 일치하는 경우
    * NON-EQUIJOIN - 한 컬럼의 값이 다른 컬럼의 값과 정확히 일치하지 않는 경우

```SQL
-- EQUI JOIN 
SELECT 
    *
FROM 
    S_EMP E, S_DEPT D
WHERE 
    E.DEPT_ID = D.ID;
    
-- ANSI INNER JOIN
SELECT 
    *
FROM 
    S_EMP E INNER JOIN S_DEPT D 
    ON E.DEPT_ID = D.ID;
```
2. OUTER JOIN

    * OUTER JOIN : 조인 테이블의 값이 존재하지 않아도 메인 테이블 데이터가 조회됨. 조인 테이블의 값을 가져오지 못하면 NULL로 표시됨.
        * LEFT OUTER JOIN - 왼쪽 테이블이 메인 테이블이 되며 조인 컬럼에 (+) 를 붙이면 해당 컬럼의 테이블이 조인 테이블이됨.
        * RIGHT OUTER JOIN - 오른쪽 테이블이 메인 테이블이 되며 조인 컬럼에
        (+) 를 붙이면 해당 컬럼의 테이블이 조인 테이블이됨. (특별한 경우가 아닌 이상 RIGHT OUTER JOIN을 사용하는 경우는 드뭄)
    * FULL OUTER JOIN : ANSI JOIN 에서만 사용하고 조인되어도 조회되고 조인이 안되어도 모두 조회됨. (자주 쓰이지는 않음)

```SQL
-- LEFT OUTER JOIN     
SELECT 
    *
FROM 
    S_EMP E, S_DEPT D 
WHERE 
    E.DEPT_ID = D.ID(+);
    
-- RIGHT OUTER JOIN
SELECT 
    *
FROM   
    S_EMP E, S_DEPT D
WHERE 
    E.DEPT_ID(+) = D.ID;
    
-- ANSI LEFT OUTER JOIN 
SELECT 
    *
FROM 
    S_EMP E LEFT OUTER JOIN S_DEPT D 
    ON E.DEPT_ID = D.ID;
    
-- ANSI RIGHT OUTER JOIN
SELECT 
    *
FROM 
    S_EMP E RIGHT OUTER JOIN S_DEPT D
    ON E.DEPT_ID = D.ID;
```     
3. SELF JOIN 

    * SELF JOIN : 1개의 테이블에 두 개의 별칭을 부여해서 2개의 테이블인 것처럼 간주한 뒤 JOIN하는 방법, 다른 컬럼을 통해서 위계 또는 관계를 알 수 있는 모습으로 조회할 수 있음.

```SQL
-- SELF JOIN
SELECT 
    W.ID 사번,
    W.NAME 사원명,
    M.ID 매니저아이디,
    M.NAME 매니저이름    
FROM 
    S_EMP W, S_EMP M
WHERE 
    W.MANAGER_ID = M.ID;

-- 김정미와 같은 직책을 가지는 사원의 이름, 직책, 급여, 부서번호 
-- 서브 쿼리 활용
SELECT
    NAME, TITLE, SALRAY, DEPT_ID
FROM 
    S_EMP
WHERE 
    1=1
    AND TITLE = (SELECT 
                    TITLE
                FROM
                    S_EMP
                WHERE
                    NAME = '김정미')
    AND NAME <> '김정미';

-- SELF JOIN 활용 
SELECT 
    E2.NAME, E2.TITLE, E2.SALARY, E2.DEPT_ID
FROM 
    S_EMP E1, S_EMP E2
WHERE
    1=1
    AND E1.TITLE = E2.TITLE
    AND E1.NAME = '김정미'
    AND E2.NAME != '김정미';
```

4. CROSS JOIN

    * CROSS JOIN : 두 테이블의 데이터가 서로 한번씩 조인되므로 테이블행은 조회된 메인 테이블과 조인 테이블의 행의 개수를 * 해줌.

```SQL
-- CROSS JOIN 
SELECT 
    *
FROM 
    S_EMP E, S_DEPT D
WHERE 
    1=1
    AND E.TITLE = '사원'
    AND D.NAME = '영업부';
    
-- ANSI CROSS JOIN 
SELECT 
    *
FROM 
    S_EMP E CROSS JOIN S_DEPT D
WHERE 
    1=1
    AND D.NAME = '영업부'
    AND E.TITLE = '사원';
```

**SET연산자**

* 중복된 건을 배제한 작업을 수행한 후에 집한 연산을 적용함.
* UNION 은 중복 작업을 진행한 뒤에 연산을 수행하므로 UNION ALL보다 쿼리 성능이 좋지 않음.(당연한 것)

1. UNION : 중복을 제거한 합집합
2. UNION ALL : 합집합
3. INTERSECT : 교집합
4. MINUS : 차집합

**SUBQUERY**

1. 스칼라 서브 쿼리 
    * SELECT 절에 사용하며, 단일 컬럼(1개의 값)을 반환함.
    * 다중 행의 값이 조회되면 오류발생.

```SQL
    SELECT 
        ID,
        NAME,
        TITLE, 
        DEPT_ID,
        (
            SELECT 
                NAME DNAME
            FROM 
                S_DEPT D
            WHERE 
                E.DEPT_ID = D.ID
                AND NAME = '기획부'
        ) DNAME
    FROM 
        S_EMP E
```

2. 인라인 뷰
    * FROM 절에 사용하며, VIEW와 사용적인 측면에서 동일함

```SQL
-- 부서별로 평균 급여보다 높은 급여를 받는 사원은?
SELECT 
    *
FROM 
(
    SELECT 
        ID,
        NAME,
        SALARY,
        DEPT_ID,
        (
        SELECT 
            AVG(SALARY)
        FROM 
            S_EMP E1
        WHERE 
            E1.DEPT_ID = E2.DEPT_ID
        GROUP BY 
            DEPT_ID
        ) AV_SALARY
    FROM 
        S_EMP E2
) A
WHERE 
    A.SALARY > A.AV_SALARY;
```

3. 중첩 서브 쿼리
    * WHERE, HAVING 절에 사용하며, 다중 컬럼 또는 다중 행을 반환함.

```SQL
-- 부서별로 평균 급여보다 높은 급여를 받는 사원은?
SELECT 
    E1.NAME,
    E1.SALARY
FROM 
    S_EMP E1
WHERE 
    E1.SALARY > 
            (
                SELECT 
                    AVG(SALARY) 평균급여
                FROM 
                    S_EMP E2
                WHERE 
                    E1.DEPT_ID = E2.DEPT_ID
                GROUP BY 
                    DEPT_ID
            );
```

**INDEX 효율적 사용**

1. INDEX가 존재하지만 사용되지 않는 경우
    * INDEX 컬럼이 비교되기 전에 변형이 일어난 경우
    * 부정(NOT, <>)으로 조건을 기술한 경우
    * INDEX 컬럼이 NULL로 비교할 경우
    * OPTIMIZER 취사선택

```SQL
-- 부정으로 조건을 기술한 경우 INDEX 타게 하는 방법
SELECT 
    ID, NAME, TITLE
FROM 
    S_EMP
WHERE 
    TITLE <> '사원';    -- INDEX 사용안됨

SELECT 
    ID, NAME, TITLE 
FROM 
    S_EMP E
WHERE
    NOT EXISTS (
                SELECT 
                    'X'
                FROM 
                    S_EMP
                WHERE 
                    E.TITLE = '사원'
               );       -- INDEX 사용됨
```

**INDEX 생성, 비생성**

1. 인덱스를 만들지 않아야 될 때
    * 테이블이 자주 변경될 때
    * 컬럼이 조회의 조건으로 사용되는 경우가 별로 없을 때
    * 인덱스는 검색속도를 증가시키지만 항상 빠른 것은 아니고, 많이 만든다고해서 좋은 것도 아님.

**VIEW**

* 간단한 뷰에서는 DML 연산 수행가능

**NVL**

**DECODE**

## ORACLE 실습

```SQL

-- CRETATE TABLE
create table TEST2 as 
(
select 
    * 
from    
    s_emp
);

CREATE TABLE TEST3
(
  ID VARCHAR2(2)  
);

-- 컬럼 추가
ALTER TABLE TEST3 ADD NAME VARCHAR(6);

-- PK 추가
ALTER TABLE TEST3 ADD PRIMARY KEY (ID);

-- PK 확인
SELECT 
    A.TABLE_NAME, A.CONSTRAINT_NAME, B.COLUMN_NAME
FROM 
    USER_CONSTRAINTS A,
    ALL_CONS_COLUMNS B
WHERE 
    1=1
    AND A.CONSTRAINT_NAME = B.CONSTRAINT_NAME
    AND A.CONSTRAINT_TYPE = 'P'
    AND A.TABLE_NAME = 'TEST3'
    AND A.OWNER = B.OWNER;

-- INSERT    
INSERT INTO TEST3
(
    ID,
    NAME,
    GENDER,
    DESCRIBE
)
VALUES 
(
    1, 
    'SON',
    'M',
    'INSERT TEST'
);

-- TABLE DATA TYPE 확인
SELECT 
    DATA_TYPE
FROM 
    COLS
WHERE 
    TABLE_NAME = 'TEST3'
    AND COLUMN_NAME = 'ID';

-- CREATE, DELETE, INSERT 변형
CREATE TABLE TEST4 AS 
SELECT * FROM S_DEPT;

DELETE FROM TEST4;

INSERT INTO TEST4 
(
    SELECT 
        *
    FROM 
        S_DEPT
);

-- UPDATE
INSERT INTO TEST4 
(
    ID, 
    NAME,
    REGION_ID
)
VALUES 
(
    12,
    'IT개발부',
    6
);

UPDATE TEST4 
    SET 
        ID = '119'
WHERE 
    NAME = 'IT개발부';

-- DISTINCT 
SELECT 
    DISTINCT NAME
FROM 
    TEST4;

-- GROUP BY 위와 결과 동일함
SELECT 
    NAME 
FROM 
    TEST4
GROUP BY 
    NAME;

-- ALIAS 두 단어로 구성되었으면 이중 따옴표 사용 
SELECT 
    NAME,
    "직장인 연봉"
FROM 
(
SELECT 
    NAME, SALARY * 12 "직장인 연봉"
FROM 
    S_EMP
);

-- GROUP BY 
-- 각 부서별 평균 급여 2000이상 부서만
SELECT
    TITLE,
    AVG(SALARY)
FROM 
    S_EMP
GROUP BY 
    TITLE
HAVING 
    AVG(SALARY) >= 2000;

-- 각 직책별 급여 총합 구하기(직책 부장인 사람 제외), 급여 총합이 3000이상인 직책만, 급여 총합에 대한 오름차순 정렬
SELECT 
    TITLE,
    MAX(SALARY) M
FROM 
    S_EMP
WHERE 
    TITLE != '부장'
GROUP BY 
    TITLE
HAVING 
    MAX(SALARY) >= 3000
ORDER BY 
    MAX(SALARY) ASC;

-- 각 부서별 직책 사원 직원들 평균급여
SELECT 
    TITLE,
    AVG(SALARY)
FROM 
    S_EMP
WHERE   
    TITLE = '사원'
GROUP BY 
    TITLE;

-- 각 부서내 각 직책별 몇 명의 인원이 있는지?
SELECT 
    TITLE,
    DEPT_ID,
    COUNT(*)
FROM 
    S_EMP
WHERE 
    TITLE IS NOT NULL
GROUP BY 
    TITLE,DEPT_ID;

-- 각 부서내에서 몇 명의 직원이 근무하는지?
SELECT 
    DEPT_ID,
    COUNT(ID) 
FROM 
    S_EMP
GROUP BY 
    DEPT_ID;

-- 각 부서별 급여의 최소값과 최대값 (같으면 출력 X)
SELECT 
    DEPT_ID,
    MIN(SALARY),
    MAX(SALARY)
FROM 
    S_EMP
GROUP BY 
    DEPT_ID
HAVING 
    MIN(SALARY) != MAX(SALARY);

-- EQUI JOIN 
SELECT 
    E.NAME, D.NAME
FROM 
    S_EMP E, S_DEPT D
WHERE 
    E.DEPT_ID = D.ID;
    
-- ANSI INNER JOIN
SELECT 
    E.NAME, D.NAME
FROM 
    S_EMP E INNER JOIN S_DEPT D 
    ON E.DEPT_ID = D.ID;

-- 직원 테이블과 부서 테이블을 JOIN하여 사원의 이름, 부서, 부서명
SELECT 
    E.NAME, E.DEPT_ID, D.NAME
FROM 
    S_EMP E, S_DEPT D
WHERE
    1=1
    AND E.DEPT_ID = D.ID;   

-- 가장 적은 평균급여를 받는 직책에 대해 그 직책과 평균급여(서브쿼리)
SELECT 
    TITLE, 
    AVG(SALARY)
FROM 
    S_EMP
HAVING
    AVG(SALARY) = (
                    SELECT 
                        MIN(AVG(SALARY))
                    FROM 
                        S_EMP
                    GROUP BY 
                        TITLE  
                  )
GROUP BY 
    TITLE; 
```