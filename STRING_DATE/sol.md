# STRING, DATE

## [자동차 대여 기록에서 장기/단기 대여 구분하기](https://school.programmers.co.kr/learn/courses/30/lessons/151138)

```sql
-- ORACLE
SELECT
    HISTORY_ID,
    CAR_ID,
    TO_CHAR(START_DATE, 'YYYY-MM-DD') AS START_DATE,
    TO_CHAR(END_DATE, 'YYYY-MM-DD') AS END_DATE,
    CASE 
        WHEN END_DATE - START_DATE >= 29 THEN '장기 대여'
        ELSE '단기 대여'
    END AS RENT_TYPE
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE TO_CHAR(START_DATE, 'YYYY-MM') = '2022-09'
ORDER BY HISTORY_ID DESC;


-- MYSQL
SELECT
    HISTORY_ID,
    CAR_ID,
    DATE_FORMAT(START_DATE, '%Y-%m-%d') AS START_DATE,
    DATE_FORMAT(END_DATE, '%Y-%m-%d') AS END_DATE,
    CASE 
        WHEN DATEDIFF(END_DATE, START_DATE) >= 29 THEN '장기 대여'
        ELSE '단기 대여'
    END AS RENT_TYPE
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE START_DATE LIKE '2022-09%'
ORDER BY HISTORY_ID DESC;
```

## [특정 옵션이 포함된 자동차 리스트 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157343?language=oracle)

```sql
-- ORACLE
SELECT 
    * 
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS LIKE '%네비게이션%'
ORDER BY CAR_ID DESC;
```

## [조건에 부합하는 중고거래 상태 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/164672?language=oracle)

```sql
-- ORACLE
SELECT 
    BOARD_ID,
    WRITER_ID,
    TITLE,
    PRICE,
    CASE 
        WHEN STATUS = 'SALE' THEN '판매중'
        WHEN STATUS = 'RESERVED' THEN '예약중'
        WHEN STATUS = 'DONE' THEN '거래완료'
    END AS STATUS
FROM USED_GOODS_BOARD
WHERE TO_CHAR(CREATED_DATE, 'YYYY-MM-DD') = '2022-10-05'
ORDER BY BOARD_ID DESC;
```

## [루시와 엘라 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59046?language=oracle)

```sql
-- ORACLE
SELECT
    ANIMAL_ID,
    NAME,
    SEX_UPON_INTAKE
FROM ANIMAL_INS
WHERE NAME = 'Lucy' OR 
      NAME = 'Ella' OR 
      NAME = 'Pickle' OR 
      NAME = 'Rogan' OR 
      NAME = 'Sabrina' OR 
      NAME = 'Mitty'
ORDER BY ANIMAL_ID
```

## [이름에 el이 들어가는 동물 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59047?language=oracle)

```sql
-- ORACLE
SELECT
    ANIMAL_ID,
    NAME
FROM ANIMAL_INS
WHERE UPPER(NAME) LIKE '%EL%' AND 
      ANIMAL_TYPE = 'Dog'
ORDER BY NAME;
```

## [중성화 여부 파악하기](https://school.programmers.co.kr/learn/courses/30/lessons/59409?language=oracle)

```sql
-- ORACLE
SELECT
    ANIMAL_ID,
    NAME,
    CASE 
        WHEN SEX_UPON_INTAKE LIKE 'Neutered%' OR
             SEX_UPON_INTAKE LIKE 'Spayed%' THEN 'O'
        ELSE 'X'
    END AS 중성화
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

## [DATETIME에서 DATE로 형 변환](https://school.programmers.co.kr/learn/courses/30/lessons/59414?language=oracle)

```sql
-- ORACLE
SELECT
    ANIMAL_ID,
    NAME,
    TO_CHAR(DATETIME, 'YYYY-MM-DD') AS 날짜
FROM ANIMAL_INS
ORDER BY ANIMAL_ID;
```

## [연도 별 평균 미세먼지 농도 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/284530)

```sql
-- ORACLE
-- 연도 별 평균 미세먼지 오염도와 (PM10)
-- 평균 초미세먼지 오염도를 조회 (PM2.5)

-- ORACLE
SELECT
    TO_CHAR(YM, 'YYYY') AS YEAR,
    ROUND(AVG(PM_VAL1), 2) AS PM10,
    ROUND(AVG(PM_VAL2), 2) AS "PM2.5"
FROM AIR_POLLUTION
WHERE LOCATION2 = '수원'
GROUP BY TO_CHAR(YM, 'YYYY')
ORDER BY YEAR;

-- MYSQL
SELECT
    YEAR(YM)AS YEAR,
    ROUND(AVG(PM_VAL1), 2) AS PM10,
    ROUND(AVG(PM_VAL2), 2) AS 'PM2.5'
FROM AIR_POLLUTION
WHERE LOCATION2 = '수원'
GROUP BY YEAR
ORDER BY YEAR;
```

## [한 해에 잡은 물고기 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/298516?language=mysql)

```sql
-- ORACLE
SELECT
    COUNT(*) AS FISH_COUNT
FROM FISH_INFO
WHERE TIME >= DATE '2021-01-01' AND
      TIME <= DATE '2022-01-01';

-- MYSQL
SELECT
    COUNT(*) AS FISH_COUNT
FROM FISH_INFO
WHERE TIME >= '2021-01-01' AND
      TIME <= '2022-01-01';

```