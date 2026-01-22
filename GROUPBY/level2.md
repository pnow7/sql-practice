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