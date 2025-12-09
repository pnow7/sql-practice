## [가격이 제일 비싼 식품의 정보 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131115?language=oracle)

```sql
SELECT 
    * 
FROM FOOD_PRODUCT
WHERE PRICE = (
            SELECT MAX(PRICE) 
            FROM FOOD_PRODUCT
      );
```

## [최솟값 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/59038)

```sql
SELECT
    MIN(DATETIME) AS DATETIME
FROM ANIMAL_INS
```

## [동물 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/59406)

```sql
SELECT
    COUNT(ANIMAL_ID) AS count
FROM ANIMAL_INS
```

## [중복 제거하기](https://school.programmers.co.kr/learn/courses/30/lessons/59408)

```sql
SELECT
    COUNT(DISTINCT NAME) AS count
FROM ANIMAL_INS
```

## [조건에 맞는 아이템들의 가격의 총합 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/273709)

```sql
SELECT
    SUM(PRICE) AS TOTAL_PRICE
FROM ITEM_INFO
WHERE RARITY = 'LEGEND';
```

## [연도별 대장균 크기의 편차 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/299310)

```sql
-- Oracle
SELECT
    TO_CHAR(DIFFERENTIATION_DATE, 'YYYY') AS YEAR,
    MAX(SIZE_OF_COLONY) OVER (
        PARTITION BY TO_CHAR(DIFFERENTIATION_DATE, 'YYYY')
    ) - SIZE_OF_COLONY AS YEAR_DEV,
    ID
FROM ECOLI_DATA
ORDER BY YEAR ASC, YEAR_DEV ASC;


-- MySQL
SELECT
    YEAR(DIFFERENTIATION_DATE) AS YEAR,
    MAX(SIZE_OF_COLONY) OVER (
        PARTITION BY YEAR(DIFFERENTIATION_DATE)
    ) - SIZE_OF_COLONY AS YEAR_DEV,
    ID
FROM ECOLI_DATA
ORDER BY 
    YEAR ASC, YEAR_DEV ASC;
```