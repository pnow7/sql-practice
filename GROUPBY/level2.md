# GROUP BY

## [가격대 별 상품 개수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131530)

- TRUNC
- → GROUP BY 에서도 설정 가능

```sql
-- ORACLE
SELECT
    TRUNC(PRICE, -4) AS PRICE_GROUP,
    COUNT(*) AS PRODUCTS
FROM PRODUCT
GROUP BY TRUNC(PRICE, -4)
ORDER BY PRICE_GROUP
```

## [입양 시각 구하기(1)](https://school.programmers.co.kr/learn/courses/30/lessons/59412)

- 1시간 단위

```sql
-- ORACLE
SELECT
    T.*
FROM (
    SELECT
        TO_NUMBER(TO_CHAR(DATETIME, 'HH24')) AS HOUR,
        COUNT(*) AS COUNT
    FROM ANIMAL_OUTS
    GROUP BY TO_NUMBER(TO_CHAR(DATETIME, 'HH24'))
) T
WHERE T.HOUR BETWEEN 9 AND 19
ORDER BY T.HOUR
```

## [성분으로 구분한 아이스크림 총 주문량](https://school.programmers.co.kr/learn/courses/30/lessons/133026)

```sql
-- ORACLE
SELECT
    T1.INGREDIENT_TYPE,
    SUM(T2.TOTAL_ORDER) AS TOTAL_ORDER
FROM ICECREAM_INFO T1
JOIN FIRST_HALF T2
  ON T1.FLAVOR = T2.FLAVOR
GROUP BY T1.INGREDIENT_TYPE
```

## [진료과별 총 예약 횟수 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/132202)

```sql
-- ORACLE
SELECT
    MCDP_CD AS "진료과코드",
    COUNT(PT_NO) AS "5월예약건수"
FROM APPOINTMENT
WHERE APNT_YMD >= TO_DATE('20220501', 'YYYYMMDD')
AND APNT_YMD < TO_DATE('20220601', 'YYYYMMDD')
GROUP BY MCDP_CD
ORDER BY "5월예약건수", "진료과코드"
```

## [자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/151137)

```sql
-- ORACLE
SELECT
    CAR_TYPE,
    COUNT(*) AS CARS
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS LIKE '%통풍시트%'
   OR OPTIONS LIKE '%열선시트%'
   OR OPTIONS LIKE '%가죽시트%'
GROUP BY CAR_TYPE
ORDER BY CAR_TYPE
```

## [고양이와 개는 몇 마리 있을까](https://school.programmers.co.kr/learn/courses/30/lessons/59040)

```sql
-- ORACLE
SELECT
    ANIMAL_TYPE,
    COUNT(*) AS COUNT
FROM ANIMAL_INS
GROUP BY ANIMAL_TYPE
ORDER BY ANIMAL_TYPE
```

## [동명 동물 수 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59041)

- NULL 처리

```sql
-- ORACLE
SELECT
    NVL(NAME, 'NONAME') AS NAME,
    COUNT(*) AS COUNT
FROM ANIMAL_INS
WHERE NAME != 'NONAME'
GROUP BY NAME
HAVING COUNT(*) >= 2
ORDER BY NAME

SELECT
    NAME,
    COUNT(NAME) AS COUNT
FROM ANIMAL_INS
GROUP BY NAME
HAVING COUNT(NAME) >= 2
ORDER BY NAME

SELECT
    NAME,
    COUNT(*) AS COUNT
FROM ANIMAL_INS
GROUP BY NAME
HAVING COUNT(*) >= 2 
   AND NAME IS NOT NULL
ORDER BY NAME;
```

## [조건에 맞는 사원 정보 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/284527)

```sql

```