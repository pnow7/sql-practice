## [경기도에 위치한 식품창고 목록 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/131114)

```sql
-- ORACLE
SELECT 
    WAREHOUSE_ID,
    WAREHOUSE_NAME,
    ADDRESS,
    NVL(FREEZER_YN, 'N') AS FREEZER_YN
FROM FOOD_WAREHOUSE
WHERE ADDRESS LIKE '경기도%'
ORDER BY WAREHOUSE_ID;

-- MYSQL
SELECT 
    WAREHOUSE_ID,
    WAREHOUSE_NAME,
    ADDRESS,
    IFNULL(FREEZER_YN, 'N') AS FREEZER_YN
FROM FOOD_WAREHOUSE
WHERE ADDRESS LIKE '경기도%'
ORDER BY WAREHOUSE_ID;
```

## [이름이 없는 동물의 아이디](https://school.programmers.co.kr/learn/courses/30/lessons/59039)

```sql
--ORACLE
SELECT 
    ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NULL
ORDER BY ANIMAL_ID

-- SELECT 
--     T.ANIMAL_ID
-- FROM (
--     SELECT
--         ANIMAL_ID,
--         NVL(NAME, 'NoName') AS NAME
--     FROM ANIMAL_INS
-- ) T
-- WHERE T.NAME = 'NoName'
-- ORDER BY T.ANIMAL_ID;
```

## [이름이 있는 동물의 아이디]https://school.programmers.co.kr/learn/courses/30/lessons/59407)

```sql
--ORACLE
SELECT
    ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
ORDER BY ANIMAL_ID;
```

## [나이 정보가 없는 회원 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131528)

```sql
--ORACLE
SELECT
    COUNT(*) AS USERS
FROM USER_INFO
WHERE AGE IS NULL
```