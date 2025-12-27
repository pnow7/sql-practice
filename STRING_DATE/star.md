## [오랜 기간 보호한 동물(2)](https://school.programmers.co.kr/learn/courses/30/lessons/59411?language=oracle)

> 두개의 테이블을 이용해서 가장 오랫동안 보호된 동물 2마리 뽑아내는 문제

```sql
-- [Oracle]
-- 입양을 간 동물 중(animal_outs), 
-- 보호기간이 가장 길었던 
-- 동물 두마리의 아이디와 이름을 조회(animal_ints)

-- 서브 쿼리
SELECT
    T3.animal_id,
    T3.name
FROM (
      SELECT 
          T1.animal_id,
          T1.name,
          T2.datetime - T1.datetime AS stay_days
      FROM animal_ins T1
      INNER JOIN animal_outs T2
      ON T1.animal_id = T2.animal_id
      ORDER BY stay_days DESC
     ) T3
WHERE ROWNUM <= 2

-- 윈도우 함수
SELECT
    animal_id,
    name
FROM (
    SELECT
        T1.animal_id,
        T1.name,
        ROW_NUMBER() OVER (
            ORDER BY T2.datetime - T1.datetime DESC
        ) AS rn
    FROM animal_ins T1
    INNER JOIN animal_outs T2
    ON T1.animal_id = T2.animal_id
)
WHERE rn <= 2;
```

## [카테고리 별 상품 개수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131529?language=oracle)

```sql
-- Oracle
SELECT
    SUBSTR(product_code, 1, 2) AS category,
    COUNT(*) AS products
FROM product
GROUP BY SUBSTR(product_code, 1, 2)
ORDER BY category
```

## [자동차 평균 대여 기간 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157342?language=oracle)

```sql
-- Oracle
SELECT
    car_id,
    TO_CHAR(ROUND(AVG(end_date - start_date + 1), 1), 'FM9999.0') AS average_duration
FROM car_rental_company_rental_history
GROUP BY car_id
HAVING AVG(end_date - start_date + 1) >= 7
ORDER BY TO_NUMBER(average_duration) DESC, car_id DESC
```

## [분기별 분화된 대장균의 개체 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/299308)

```sql
-- Oracle (TO_CHAR(date, 'Q') -> 1 ~ 4 반환)
SELECT
    TO_CHAR(diffrentiation_date, 'Q') || 'Q' AS quarter,
    COUNT(*) AS ecoli_count
FROM ecoli_info
GROUP BY TO_CHAR(diffrentiation_date, 'Q')
ORDER BY TO_CHAR(diffrentiation_date, 'Q');

-- MySQL (QUARTER() 함수 사용)
SELECT
    CONCAT(q, 'Q') AS QUARTER,
    COUNT(*) AS ECOLI_COUNT
FROM (
    SELECT QUARTER(DIFFERENTIATION_DATE) AS q
    FROM ECOLI_DATA
) t
GROUP BY q
ORDER BY q;
```