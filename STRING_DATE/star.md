## [오랜 기간 보호한 동물(2)](https://school.programmers.co.kr/learn/courses/30/lessons/59411?language=oracle)

> 두개의 테이블을 이용해서 가장 오랫동안 보호된 동물 2마리 뽑아내는 문제

```sql
-- ORACLE
-- 입양을 간 동물 중(ANIMAL_OUTS), 
-- 보호기간이 가장 길었던 
-- 동물 두마리의 아이디와 이름을 조회(ANIMAL_INTS)

-- 서브 쿼리
SELECT
    T3.ANIMAL_ID,
    T3.NAME
FROM (
      SELECT 
          T1.ANIMAL_ID,
          T1.NAME,
          T2.DATETIME - T1.DATETIME AS STAY_DAYS
      FROM ANIMAL_INS T1
      INNER JOIN ANIMAL_OUTS T2
      ON T1.ANIMAL_ID = T2.ANIMAL_ID
      ORDER BY STAY_DAYS DESC
     ) T3
WHERE ROWNUM <= 2

-- 윈도우 함수
SELECT
    ANIMAL_ID,
    NAME
FROM (
    SELECT
        T1.ANIMAL_ID,
        T1.NAME,
        ROW_NUMBER() OVER (
            ORDER BY T2.DATETIME - T1.DATETIME DESC
        ) AS RN
    FROM ANIMAL_INS T1
    INNER JOIN ANIMAL_OUTS T2
    ON T1.ANIMAL_ID = T2.ANIMAL_ID
)
WHERE RN <= 2;
```

## [카테고리 별 상품 개수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131529?language=oracle)

```sql
-- ORACLE
SELECT
    SUBSTR(PRODUCT_CODE, 1, 2) AS CATEGORY,
    COUNT(*) AS PRODUCTS
FROM PRODUCT
GROUP BY SUBSTR(PRODUCT_CODE, 1, 2)
ORDER BY CATEGORY
```

## [자동차 평균 대여 기간 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157342?language=oracle)

```sql
-- ORACLE
SELECT
    CAR_ID,
    TO_CHAR(ROUND(AVG(END_DATE - START_DATE + 1), 1), 'FM9999.0') AS AVERAGE_DURATION
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY CAR_ID
HAVING AVG(END_DATE - START_DATE + 1) >= 7
ORDER BY TO_NUMBER(AVERAGE_DURATION) DESC, CAR_ID DESC
```

## [분기별 분화된 대장균의 개체 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/299308)

```sql
-- ORACLE (TO_CHAR(DATE, 'Q') -> 1 ~ 4 반환)
SELECT
    TO_CHAR(DIFFRENTIATION_DATE, 'Q') || 'Q' AS QUARTER,
    COUNT(*) AS ECOLI_COUNT
FROM ECOLI_INFO
GROUP BY TO_CHAR(DIFFRENTIATION_DATE, 'Q')
ORDER BY TO_CHAR(DIFFRENTIATION_DATE, 'Q');

-- MYSQL (QUARTER() 함수 사용)
SELECT
    CONCAT(Q, 'Q') AS QUARTER,
    COUNT(*) AS ECOLI_COUNT
FROM (
    SELECT QUARTER(DIFFERENTIATION_DATE) AS Q
    FROM ECOLI_DATA
) T
GROUP BY Q
ORDER BY Q;
```