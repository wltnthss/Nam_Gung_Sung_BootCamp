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

**CONSTRAINT**

* 데이터의 무결성을 지키기 위해 제한된 조건
* 즉, 테이블이나 속성에 부적절한 데이터가 들어오는 것을 사전에 차단하도록 정해 놓은 것

* NOT NULL
    * NULL값 설정 불가
* UNIQUE
    * 중복간 설정 불가
* CHECK
    * 지정한 조건에 맞지 않는 값은 설정할 수 없음.
* PRIMARY KEY
    * 테이블에는 단 하나의 PK만 허용됨.
    * UNIQUE 컬럼에 대한 인덱스가 자동 생성됨.
    * 중복값과 NULL값 설정 불가
* FOREIGN KEY
    * 부모 테이블의 값과 일치하거나 NULL 이어야함.
    * 참조하고자 하는 컬럼이 PK 또는 UNIQUE 제약조건이 있어야함.
* DEFAULT

```SQL
-- 제약 조건 조회
SELECT * FROM USER_CONSTRAINTS WHERE TABLE_NAME = 'S_EMP';

-- 제약 조건 추가
ALTER TABLE S_EMP MODIFY MAILID NOT NULL;
ALTER TABLE S_EMP ADD CONSTRAINT UNIQUE_MAILID UNIQUE(MAILID);
ALTER TABLE S_EMP ADD CONSTRAINT PK_ID PRIMARY KEY(ID);

-- 제약 조건 삭제
ALTER TABLE S_EMP DROP CONSTRAINT PK_S_EMP;
ALTER TABLE S_EMP DROP CONSTRAINT UNIQUE_MAILID;
```

**DICTIONARY**

* 데이터베이스에 대한 정보를 가짐
* ORACLE SERVER에 의해서 생성되고 유지보수

**SEQUENCE**

* 오라클에서는 자동 증가 컬럼을 사용할 수가 없음.
* 때문에 오라클에서 컬럼의 값을 증가시키기 위해서는 주로 시퀀스를 사용함

* INCREMENT BY : 시퀀스 실행 시 증가시킬 값
* START WITH : 시퀀스의 시작값이다. (MINVALUE과 같거나 커야 한다)
* MINVALUE : 시퀀스가 시작되는 최솟값이다.
* MAXVALUE : 시퀀스가 끝나는 최댓값이다.
* NOCYCLE | CYCLE : NOCYCLE (반복안함), CYCLE(시퀀스의 최댓값에 도달 시 최솟값 1부터 다시시작)
* NOCACHE | CACHE : NOCACHE(사용안함), CACHE(캐시를 사용하여 미리 값을 할당해 놓아서 속도가 빠르며, 동시 사용자가 많을 경우 유리)
* NOORDER | ORDER : NOORDER(사용안함), ORDER(요청 순서로 값을 생성하여 발생 순서를 보장하지만 조금의 시스템 부하가 있음)

```SQL
-- 해당 유저에 생성된 모든 시퀀스 확인 방법
SELECT * FROM user_sequences;

-- SEQUENCE 생성
CREATE SEQUENCE ID
    INCREMENT BY 1
    START WITH 26
    MINVALUE 1
    MAXVALUE 99999
    NOCYCLE
    NOCACHE
    NOORDER;

-- SEQUENCE 삭제
DROP SEQUENCE ID;

-- SEQUENCE 수정
ALTER SEQUENCE ID MAXVALUE 9999;
ALTER SEQUENCE ID INCREMENT BY 2;

-- SEQUENCE 사용, NEXTVAL을 사용하여 일련번호를 생성할 수 있음.
SELECT 
    ID.NEXTVAL
FROM 
    DUAL;
```
**INDEX**

* 테이블의 데이터를 좀 더 빠르게 검색하기 위해 사용하는 데이터베이스 Object.
* ORACLE SERVER 가 최적화 방법을 따라 어떤 Index를 사용할 것인지, 사용하지 않을 것인지 결정
* B+Tree 의 검색방법으로 디스크 입출력 횟수를 줄임.
* 자동으로 생성되기도 하고 사용자가 필요에 의해 만들기도함.
* INDEX는 논리적, 물리적으로 테이블과는 독립적임.
* ORACLE SERVER가 자동적으로 INDEX를 사용하고 유지보수함.
* 인덱스는 검색속도를 증가시키지만 항상 빠른 것은 아니고, 많이 만든다고해서 좋은 것도 아님.
* 테이블과 연관된 인덱스가 많을 수록 오라클 서버 부담은 증가함.

```SQL
-- INDEX 조회
SELECT * FROM IND;

-- INDEX 생성
-- CREATE INDEX INDEX_NAME ON TABLE_NAME(COLUMN...)
CREATE INDEX T_INDEX ON S_EMP(NAME);
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

1. 인덱스 생성 권장 X
    * 테이블이 자주 변경될 때
    * 컬럼이 조회의 조건으로 사용되는 경우가 별로 없을 때
    * 테이블이 작거나, 조회가 행의 10% 정도 이상을 검색할 때
2. 인덱스 생성 권장 O
    * 컬럼에 NULL값이 많이 포함되있을 때
    * 1개 이상의 컬럼이 함께 WHERE, JOIN조건으로 자주 사용될 때
    * 테이블이 크고, 테이블에서 조회되는 행의 수가 전체의 10%정도 일 때

**VIEW**

* 간단한 뷰에서는 DML 연산 수행가능
* 테이블이나 다른 뷰를 기초로 한 가상의 테이블
* 선택적인 내용을 보여줌으로써 데이터베이스에 대한 액세스를 제한함.(보안적인 강점)
* 한 개의 뷰로 여러 테이블에 대한 데이터 검색 가능
* UNION, JOIN, GROUP BY 를 사용한 쿼리는 DML 사용 불가함.

```SQL
-- VIEW 생성
CREATE OR REPLACE VIEW MY_VIEW AS
(
SELECT 
    *
FROM 
    S_EMP
);
-- VIEW 조회
SELECT * FROM MY_VIEW;
SELECT * FROM USER_VIEWS;

-- VIEW 삭제
DROP VIEW MY_VIEW;
```

**SYNONYM**

* ALIAS 같이 이름을 줄여주는 역할이며 테이블의 이름을 설정해주는 것
* 특정 OBJECT에 부여하는 또 다른 이름이며 사용자의 편의나 참조를 빠르게 하기 위해 사용함.
* 

```SQL
CREATE [OR REPLACE] [PUBLIC]
SYNONYM '[스키마명].시노님명'
    FOR '스키마명.대상오브젝트명'

-- 시노님 생성
CREATE SYNONYM MY_EMP FOR S_EMP;

-- 시노님 조회
SELECT * FROM MY_EMP;

-- 시노님 삭제
DROP SYNONYM MY_EMP;
```

**NVL**

* NULL 값을 포함하는 컬럼을 지정된 값으로 변경하는데 사용함.
* NVL(형식1, 형식2) - 형식 1 : NULL값 포함 컬럼, 형식 2 : 변경하려는 값
* NVL2(형식1, 형식2, 형식 3) - NULL이면 형식3, 아니면 형식2를 출력함.

```SQL
SELECT ID, NAME, NVL(REGION_ID, 10) FROM S_DEPT;
SELECT ID, NAME, NVL2(REGION_ID, 20, 30) FROM S_DEPT;
```

**DECODE**

* 값을 비교하여 해당하는 값을 돌려주는 함수
* CASE WHEN THEN 을 사용하지만 오라클에서는 DECODE를 자주 사용함.
* DECODE(형식, 비교값1, 결과치1, 기본치)

```SQL
SELECT 
    SALARY,
    DECODE(SALARY/1000, 0, 'E', 'A')    -- 0이면 'E', 아니면 'A'
FROM 
    S_EMP;
```

**TRIGGER**

* 임의의 테이블에 DML이 수행 됐을 때, 데이터베이스에서 **자동적으로 동작하도록 작성된 프로그램**임.
* 테이블과 별도로 데이터베이스에 저장됨.

```SQL
CREATE [ OR REPLACE ] TRIGGER 트리거명
BEFORE | AFTER
[ 동작(INSERT, UPDATE, DELETE) ] ON 테이블명 
[ REFERENCING  NEW | OLD  TABLE AS 테이블명 ]
[ FOR EACH ROW ]
[ WHEN 조건식 ]
트리거 BODY문

CREATE OR REPLACE TRIGGER oracle_trigger
   BEFORE
   INSERT ON oracleStudy
   REFERENCING NEW TABLE AS new_trigger
   FOR EACH ROW
   WHEN new_trigger.점수 = ''
   BEGIN
     SET new_table.점수 = '0';
   END;
```

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


-- PIVOT
SELECT 
    *
FROM 
    (
        SELECT 
            ID, 
            TO_CHAR(START_DATE, 'MM') || '월' YYM
        FROM 
            S_EMP
    )
PIVOT
    (
        COUNT(*)
        FOR YYM IN ('01월', '02월', '03월')
    );

-- DECODE
SELECT 
    ID,
    SUM(DECODE(TO_CHAR(START_DATE, 'MM'), '01', 1, 0)) "1월",
    SUM(DECODE(TO_CHAR(START_DATE, 'MM'), '02', 1, 0)) "2월",
    SUM(DECODE(TO_CHAR(START_DATE, 'MM'), '03', 1, 0)) "3월"
FROM 
    S_EMP
GROUP BY 
    ID;

-- ROLLUP 그룹별 합계
SELECT 
    DEPT_ID, TITLE, COUNT(*)
FROM 
    S_EMP
GROUP BY 
    ROLLUP(DEPT_ID, TITLE);
    
-- CUBE 그룹별 합계 및 소계
SELECT 
    DEPT_ID, TITLE, COUNT(*)
FROM 
    S_EMP
GROUP BY 
    CUBE(DEPT_ID, TITLE)
ORDER BY 
    DEPT_ID;

-- RANK 행별 순위 계산
SELECT 
    ID, 
    NAME, 
    DEPT_ID, 
    SALARY , 
    RANK() OVER(PARTITION BY DEPT_ID ORDER BY SALARY) RANK
FROM 
    S_EMP;

-- 자신의 급여가 자신이 속한 부서의 평균 급여보다 적은 직원의 이름, 급여, 부서번호
SELECT 
    NAME, DEPT_ID, SALARY
FROM 
    S_EMP E1
WHERE 
    SALARY < 
            (
            SELECT 
                AVG(SALARY)
            FROM 
                S_EMP E2
            WHERE 
                E1.DEPT_ID = E2.DEPT_ID
            GROUP BY 
                DEPT_ID
            )
;

-- 본인의 급여가 각 부서별 평균 급여 중 어느 한 부서의 평균 급여보다 적은 급여를 받는 직원에 대해 이름, 급여, 부서번호를 출력하시오
SELECT 
    NAME, SALARY, DEPT_ID
FROM 
    S_EMP E1
WHERE
    SALARY < ANY(
                SELECT 
                    AVG(SALARY)
                FROM 
                    S_EMP E2
                GROUP BY 
                    DEPT_ID
                );

-- 본인이 다른 사람의 관리자로 되어 있는 직원의 사번, 이름, 직책, 부서번호
SELECT 
    ID, NAME, TITLE, DEPT_ID
FROM 
    S_EMP E1
WHERE 
    EXISTS (
            SELECT 
                ID
            FROM 
                S_EMP E2
            WHERE 
                E1.ID = E2.MANAGER_ID
            );
```